<script setup>
import { ref, shallowRef, onMounted, watch, nextTick, onBeforeUnmount } from 'vue'
import * as pdfjsLib from 'pdfjs-dist'
import pdfWorker from 'pdfjs-dist/build/pdf.worker?url'

/* =========================
   PDF WORKER
========================= */
pdfjsLib.GlobalWorkerOptions.workerSrc = pdfWorker

/* =========================
   PROPS
========================= */
const props = defineProps({
  src: { type: String, required: true }
})

/* =========================
   STATE
========================= */
const scrollRef = ref(null)
const pdfDoc = shallowRef(null)

const scale = ref(1)
const totalPages = ref(0)
const currentPage = ref(1)
const pageInput = ref('1')

const showSidebar = ref(false)
const thumbs = ref([]) // [{ page, url }]

const MIN_SCALE = 0.6
const MAX_SCALE = 3
const STEP = 0.1

let observer = null
let isRendering = false
let renderToken = 0

// Used to prevent “flash to top” during zoom
const freeze = ref(false)

/* =========================
   UTILS
========================= */
function clamp(n, min, max) {
  return Math.max(min, Math.min(max, n))
}
function round1(n) {
  return Math.round(n * 10) / 10
}

/**
 * Capture anchor based on scroll viewport center:
 * page + ratio (0..1) inside that page.
 */
function captureAnchor() {
  const sc = scrollRef.value
  if (!sc) return { page: currentPage.value, ratio: 0.5 }

  const pages = Array.from(sc.querySelectorAll('.pdf-page'))
  if (!pages.length) return { page: currentPage.value, ratio: 0.5 }

  const centerY = sc.scrollTop + sc.clientHeight / 2

  let bestEl = pages[0]
  let bestDist = Infinity

  for (const el of pages) {
    const mid = el.offsetTop + el.clientHeight / 2
    const dist = Math.abs(centerY - mid)
    if (dist < bestDist) {
      bestDist = dist
      bestEl = el
    }
  }

  const page = Number(bestEl.dataset.page)
  const ratio = bestEl.clientHeight
    ? clamp((centerY - bestEl.offsetTop) / bestEl.clientHeight, 0, 1)
    : 0.5

  return { page, ratio }
}

/**
 * Restore anchor so same visual point stays centered.
 * Must be called AFTER pages exist.
 */
function restoreAnchor(anchor) {
  const sc = scrollRef.value
  if (!sc) return

  const el = sc.querySelector(`.pdf-page[data-page="${anchor.page}"]`)
  if (!el) return

  const yWithin = anchor.ratio * el.clientHeight
  const target = el.offsetTop + yWithin - sc.clientHeight / 2
  sc.scrollTo({ top: Math.max(0, target), behavior: 'auto' })
}

/* =========================
   OBSERVER (page tracking)
========================= */
function setupObserver() {
  const sc = scrollRef.value
  if (!sc) return

  observer?.disconnect()

  observer = new IntersectionObserver(
    entries => {
      if (isRendering) return

      // choose most-visible page to avoid flicker
      let best = null
      for (const e of entries) {
        if (!e.isIntersecting) continue
        if (!best || e.intersectionRatio > best.intersectionRatio) best = e
      }
      if (!best) return

      const p = Number(best.target.dataset.page)
      if (!Number.isFinite(p)) return

      currentPage.value = p
      pageInput.value = String(p)
    },
    { root: sc, threshold: [0.35, 0.55, 0.75] }
  )

  sc.querySelectorAll('.pdf-page').forEach(p => observer.observe(p))
}

/* =========================
   THUMBNAILS
========================= */
async function buildThumbnails() {
  // cleanup old URLs
  thumbs.value.forEach(t => t?.url && URL.revokeObjectURL(t.url))
  thumbs.value = []

  if (!pdfDoc.value) return

  // small scale thumbnails
  const thumbScale = 0.18

  for (let i = 1; i <= totalPages.value; i++) {
    const page = await pdfDoc.value.getPage(i)

    const viewport = page.getViewport({ scale: thumbScale })
    const canvas = document.createElement('canvas')
    const ctx = canvas.getContext('2d')

    canvas.width = Math.floor(viewport.width)
    canvas.height = Math.floor(viewport.height)

    await page.render({ canvasContext: ctx, viewport }).promise

    const blob = await new Promise(resolve => canvas.toBlob(resolve, 'image/webp', 0.85))
    const url = URL.createObjectURL(blob)

    thumbs.value.push({ page: i, url })
  }
}

/* =========================
   LOAD PDF
========================= */
async function loadPdf() {
  const token = ++renderToken
  isRendering = true
  freeze.value = true

  try {
    pdfDoc.value = await pdfjsLib.getDocument(props.src).promise
    if (token !== renderToken) return

    totalPages.value = pdfDoc.value.numPages
    currentPage.value = 1
    pageInput.value = '1'

    // render pages first (so user can see quickly)
    await renderPages(true)

    // thumbnails build after (non-blocking feel)
    // still awaited here for simplicity; you can change later
    await buildThumbnails()
  } finally {
    // renderPages handles unfreezing at the right time
  }
}

/* =========================
   RENDER ALL PAGES
   - No flash to top (freeze)
   - Keeps anchor on zoom
========================= */
async function renderPages(resetScroll = false) {
  const sc = scrollRef.value
  if (!sc || !pdfDoc.value) return

  const token = ++renderToken

  // freeze UI so it doesn't show top before restore
  freeze.value = true
  isRendering = true

  const anchor = resetScroll ? { page: 1, ratio: 0.5 } : captureAnchor()

  // cleanup
  observer?.disconnect()
  observer = null
  sc.innerHTML = ''

  for (let i = 1; i <= totalPages.value; i++) {
    if (token !== renderToken) return

    const page = await pdfDoc.value.getPage(i)
    const viewport = page.getViewport({ scale: scale.value })

    const canvas = document.createElement('canvas')
    const ctx = canvas.getContext('2d')

    canvas.width = Math.floor(viewport.width)
    canvas.height = Math.floor(viewport.height)

    const wrap = document.createElement('div')
    wrap.className = 'pdf-page'
    wrap.dataset.page = String(i)
    wrap.appendChild(canvas)

    sc.appendChild(wrap)

    await page.render({ canvasContext: ctx, viewport }).promise
  }

  if (token !== renderToken) return

  await nextTick()
  setupObserver()

  // restore anchor BEFORE showing
  restoreAnchor(anchor)

  // show after browser has applied scroll position
  requestAnimationFrame(() => {
    requestAnimationFrame(() => {
      freeze.value = false
      isRendering = false

      // ensure pageInput is consistent
      const a = captureAnchor()
      currentPage.value = a.page
      pageInput.value = String(a.page)
    })
  })
}

/* =========================
   CONTROLS
========================= */
function zoomIn() {
  if (isRendering) return
  const next = round1(clamp(scale.value + STEP, MIN_SCALE, MAX_SCALE))
  if (next !== scale.value) scale.value = next
}

function zoomOut() {
  if (isRendering) return
  const next = round1(clamp(scale.value - STEP, MIN_SCALE, MAX_SCALE))
  if (next !== scale.value) scale.value = next
}

function goToPage() {
  const sc = scrollRef.value
  if (!sc) return

  let p = Number(pageInput.value)
  if (!Number.isFinite(p)) {
    pageInput.value = String(currentPage.value)
    return
  }

  p = clamp(p, 1, totalPages.value)
  currentPage.value = p
  pageInput.value = String(p)

  const el = sc.querySelector(`.pdf-page[data-page="${p}"]`)
  if (el) sc.scrollTo({ top: Math.max(0, el.offsetTop - 24), behavior: 'smooth' })
}

function jumpToPage(p) {
  pageInput.value = String(p)
  goToPage()
}

function downloadPdf() {
  const a = document.createElement('a')
  a.href = props.src
  a.download = 'document.pdf'
  a.click()
}

/* =========================
   WATCHERS
========================= */
watch(scale, () => renderPages(false))
watch(() => props.src, () => loadPdf())

/* =========================
   LIFECYCLE
========================= */
onMounted(loadPdf)

onBeforeUnmount(() => {
  observer?.disconnect()
  observer = null
  thumbs.value.forEach(t => t?.url && URL.revokeObjectURL(t.url))
})
</script>

<template>
  <div class="pdf-root">
    <!-- ===== TOOLBAR (KEEP COLORS) ===== -->
    <div class="pdf-toolbar">
      <div class="tb-left">
        <button class="tb-btn" @click="showSidebar = !showSidebar" title="Menu">☰</button>

        <div class="page-input">
          <input v-model="pageInput" @keyup.enter="goToPage" />
          <span>/ {{ totalPages }}</span>
        </div>
      </div>

      <div class="tb-mid">
        <button class="tb-btn" @click="zoomOut" title="Zoom out">−</button>
        <span class="zoom-text">{{ Math.round(scale * 100) }}%</span>
        <button class="tb-btn" @click="zoomIn" title="Zoom in">+</button>
      </div>

      <div class="tb-right">
        <button class="tb-btn" @click="downloadPdf" title="Download">⬇</button>
        <button class="tb-btn" disabled title="Share (coming)">⤴</button>
      </div>
    </div>

    <!-- ===== BODY ===== -->
    <div class="pdf-body">
      <!-- Sidebar with thumbnails -->
      <aside class="pdf-sidebar" :class="{ open: showSidebar }">
        <div class="sb-title">All pages</div>

        <div class="sb-list">
          <button
            v-for="t in thumbs"
            :key="t.page"
            class="sb-thumb"
            :class="{ active: t.page === currentPage }"
            @click="jumpToPage(t.page)"
          >
            <div class="thumb-img">
              <img :src="t.url" :alt="'Page ' + t.page" />
            </div>
            <div class="thumb-label">{{ t.page }}</div>
          </button>

          <!-- fallback if thumbs still loading -->
          <div v-if="!thumbs.length" class="sb-loading">
            Loading pages…
          </div>
        </div>
      </aside>

      <!-- PDF area (freeze prevents flash-to-top) -->
      <div class="pdf-view">
        <div
          ref="scrollRef"
          class="pdf-scroll"
          :class="{ frozen: freeze }"
        ></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* ========= KEEP OLD COLORS, ONLY IMPROVE UI ========= */

.pdf-root {
  height: 100%;
  width: 100%;
  background: #2b2b2b;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.pdf-toolbar {
  height: 56px;
  background: #3a3a3a;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 14px;
  gap: 12px;
}

.tb-left, .tb-mid, .tb-right {
  display: flex;
  align-items: center;
  gap: 10px;
}

.tb-btn {
  width: 38px;
  height: 38px;
  border-radius: 10px;
  border: none;
  background: rgba(255,255,255,.06);
  color: #fff;
  cursor: pointer;
  font-size: 18px;
  display: grid;
  place-items: center;
}
.tb-btn:hover { background: rgba(255,255,255,.12); }
.tb-btn:disabled { opacity: .35; cursor: not-allowed; }

.zoom-text {
  width: 62px;
  text-align: center;
  font-size: 13px;
  opacity: .9;
}

.page-input {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  opacity: .95;
}
.page-input input {
  width: 56px;
  padding: 6px 8px;
  background: #222;
  color: #fff;
  border: none;
  border-radius: 8px;
  text-align: center;
  outline: none;
}

/* Body layout */
.pdf-body {
  flex: 1;
  display: grid;
  grid-template-columns: auto 1fr;
  height: calc(100% - 56px);
}

/* Sidebar */
.pdf-sidebar {
  width: 0;
  overflow: hidden;
  background: #1f1f1f;
  color: #fff;
  transition: width .2s ease;
  border-right: 1px solid rgba(255,255,255,.06);
}
.pdf-sidebar.open { width: 260px; }

.sb-title {
  padding: 14px 14px 8px;
  font-size: 13px;
  opacity: .8;
}

.sb-list {
  padding: 10px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 12px;
  overflow: auto;
  height: calc(100% - 40px);
}

.sb-thumb {
  border: none;
  background: rgba(255,255,255,.06);
  border-radius: 12px;
  padding: 10px;
  cursor: pointer;
  color: #fff;
  display: grid;
  gap: 8px;
}
.sb-thumb:hover { background: rgba(255,255,255,.12); }
.sb-thumb.active { background: rgba(255,255,255,.18); }

.thumb-img {
  background: rgba(0,0,0,.25);
  border-radius: 10px;
  padding: 8px;
  display: grid;
  place-items: center;
}
.thumb-img img {
  width: 100%;
  height: auto;
  border-radius: 6px;
  display: block;
}

.thumb-label {
  font-size: 12px;
  opacity: .85;
  text-align: center;
}

.sb-loading {
  font-size: 13px;
  opacity: .7;
  padding: 10px;
}

/* PDF view */
.pdf-view {
  height: 100%;
  overflow: hidden;
}

/* Scroll area */
.pdf-scroll {
  height: 100%;
  overflow-y: auto;
  padding: 28px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 36px;
}

/* ✅ This is the "no flash to page 1" fix */
.pdf-scroll.frozen {
  visibility: hidden;
}

.pdf-page {
  display: flex;
  justify-content: center;
  width: 100%;
}
.pdf-page canvas {
  background: #fff;
  box-shadow: 0 16px 40px rgba(0,0,0,.35);
  border-radius: 2px;
}
</style>
