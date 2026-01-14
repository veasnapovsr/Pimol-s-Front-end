<script setup>
import { ref, shallowRef, onMounted, watch, nextTick } from 'vue'
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
let observer

/* =========================
   LOAD PDF
========================= */
async function loadPdf() {
  pdfDoc.value = await pdfjsLib.getDocument(props.src).promise
  totalPages.value = pdfDoc.value.numPages
  pageInput.value = '1'
  await renderPages()
}

/* =========================
   RENDER ALL PAGES
========================= */
async function renderPages() {
  if (!scrollRef.value || !pdfDoc.value) return

  scrollRef.value.innerHTML = ''
  if (observer) observer.disconnect()

  for (let i = 1; i <= totalPages.value; i++) {
    const page = await pdfDoc.value.getPage(i)
    const viewport = page.getViewport({ scale: scale.value })

    const canvas = document.createElement('canvas')
    const ctx = canvas.getContext('2d')

    canvas.width = viewport.width
    canvas.height = viewport.height

    const pageWrap = document.createElement('div')
    pageWrap.className = 'pdf-page'
    pageWrap.dataset.page = i
    pageWrap.appendChild(canvas)

    scrollRef.value.appendChild(pageWrap)

    await page.render({ canvasContext: ctx, viewport }).promise
  }

  await nextTick()
  observeScroll()
}

/* =========================
   SCROLL TRACKING
========================= */
function observeScroll() {
  observer = new IntersectionObserver(
    entries => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          currentPage.value = Number(e.target.dataset.page)
          pageInput.value = String(currentPage.value)
        }
      })
    },
    { root: scrollRef.value, threshold: 0.6 }
  )

  scrollRef.value.querySelectorAll('.pdf-page')
    .forEach(p => observer.observe(p))
}

/* =========================
   CONTROLS
========================= */
const zoomIn = () => scale.value = Math.min(scale.value + 0.1, 3)
const zoomOut = () => scale.value = Math.max(scale.value - 0.1, 0.5)

function goToPage() {
  let page = Number(pageInput.value)
  if (isNaN(page)) return
  page = Math.max(1, Math.min(page, totalPages.value))

  const el = scrollRef.value.querySelector(`.pdf-page[data-page="${page}"]`)
  if (el) {
    const top =
      el.offsetTop -
      scrollRef.value.clientHeight / 2 +
      el.clientHeight / 2

    scrollRef.value.scrollTo({ top, behavior: 'smooth' })
  }
}

function downloadPdf() {
  const a = document.createElement('a')
  a.href = props.src
  a.download = 'document.pdf'
  a.click()
}

/* =========================
   LIFECYCLE
========================= */
onMounted(loadPdf)
watch(scale, renderPages)
</script>

<template>
  <div class="pdf-root">

    <!-- ===== TOOLBAR ===== -->
    <div class="pdf-toolbar">
      <!-- Page -->
      <div class="page-input">
        <input
          v-model="pageInput"
          @keyup.enter="goToPage"
        />
        <span>/ {{ totalPages }}</span>
      </div>

      <!-- Zoom -->
      <div class="zoom-controls">
        <button @click="zoomOut">−</button>
        <span>{{ Math.round(scale * 100) }}%</span>
        <button @click="zoomIn">+</button>
      </div>

      <!-- Actions -->
      <div class="actions">
        <button @click="downloadPdf">⬇</button>
        <button disabled>⤴</button>
      </div>
    </div>

    <!-- ===== SCROLL AREA ===== -->
    <div ref="scrollRef" class="pdf-scroll"></div>

  </div>
</template>

<style scoped>
/* ===== ROOT ===== */
.pdf-root {
  height: 100%;
  width: 100%;
  border: 1.5px solid #000;
  border-radius: 16px;
  background: #f3f4f6;
  overflow: hidden;
}

/* ===== TOOLBAR ===== */
.pdf-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #fff;
  border-bottom: 1.5px solid #000;
  padding: 10px 16px;
}

/* Page input */
.page-input {
  display: flex;
  align-items: center;
  gap: 6px;
}
.page-input input {
  width: 52px;
  padding: 4px 6px;
  border: 1px solid #000;
  border-radius: 6px;
  text-align: center;
}

/* Zoom */
.zoom-controls {
  display: flex;
  align-items: center;
  gap: 10px;
}
.zoom-controls button {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  border: 1px solid #d1d5db;
  background: #fff;
}

/* Actions */
.actions button {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  border: 1px solid #d1d5db;
  background: #fff;
}
.actions button:disabled {
  opacity: 0.4;
}

/* ===== SCROLL AREA ===== */
.pdf-scroll {
  height: calc(100% - 56px);
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 32px;
  padding: 32px 0;
}

/* ===== PAGE ===== */
.pdf-page {
  display: flex;
  justify-content: center;
  width: 100%;
}
.pdf-page canvas {
  background: #fff;
  box-shadow: 0 12px 28px rgba(0,0,0,.15);
}
</style>
