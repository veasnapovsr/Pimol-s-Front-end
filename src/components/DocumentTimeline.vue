<template>
  <div class="bg-white rounded-2xl border p-6 h-full">

    <!-- TITLE -->
    <h3 class="text-lg font-semibold mb-6">
      ស្ថានភាពដំណើរការឯកសារ
    </h3>

    <!-- TIMELINE -->
    <div class="space-y-6">

      <div
        v-for="(step, index) in steps"
        :key="step.id"
        class="flex gap-4"
      >
        <!-- LEFT ICON + LINE -->
        <div class="relative flex flex-col items-center">

          <!-- ICON -->
          <div
            class="w-9 h-9 rounded-full flex items-center justify-center"
            :class="circleClass(index)"
          >
            <!-- GREEN -->
            <svg
              v-if="stepStatus(index) === 'green'"
              viewBox="0 0 24 24"
              class="w-4 h-4 text-green-600"
              fill="none"
              stroke="currentColor"
              stroke-width="3"
            >
              <path d="M5 13l4 4L19 7" />
            </svg>

            <!-- YELLOW -->
            <svg
              v-else-if="stepStatus(index) === 'yellow'"
              viewBox="0 0 24 24"
              class="w-4 h-4 text-yellow-600"
              fill="none"
              stroke="currentColor"
              stroke-width="3"
            >
              <circle cx="12" cy="12" r="9" />
            </svg>

            <!-- RED -->
            <svg
              v-else
              viewBox="0 0 24 24"
              class="w-4 h-4 text-red-600"
              fill="none"
              stroke="currentColor"
              stroke-width="3"
            >
              <path d="M6 18L18 6M6 6l12 12" />
            </svg>
          </div>

          <!-- LINE -->
          <div
            v-if="index < steps.length - 1"
            class="w-px flex-1 mt-1 border-dashed"
            :class="lineClass(index)"
          ></div>
        </div>

        <!-- CONTENT -->
        <div class="flex-1">
          <div class="flex justify-between">
            <p class="font-semibold" :class="textClass(index)">
              {{ step.title }}
            </p>
            <span class="text-sm text-gray-400">
              {{ step.time }}
            </span>
          </div>

          <p class="text-sm text-gray-500">
            {{ step.subtitle }}
          </p>
        </div>
      </div>

      <!-- COMMENT (ONLY WHEN YELLOW OR RED EXISTS) -->
      <div v-if="showComment" class="pt-4">
        <label class="block font-semibold mb-2 text-yellow-600">
          មតិយោបល់
        </label>

        <textarea
          v-model="comment"
          rows="3"
          placeholder="បញ្ចូលមតិយោបល់..."
          class="w-full rounded-lg border p-3 text-sm focus:ring-2 focus:ring-blue-500"
        />

        <div class="text-right mt-3">
          <button
            class="inline-flex items-center gap-2 bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg text-sm"
          >
            ➤ បញ្ជូនមតិយោបល់
          </button>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

/* ================= INPUT FROM API ================= */
/*
  1  = approved (green)
  0  = pending (yellow)
 -1  = rejected (red)
*/
const stepsStatus = ref([1, 1, -1, 1]) // 👈 change this to test

/* ================= DATA ================= */
const comment = ref('')

const steps = [
  {
    id: 1,
    title: 'បានបញ្ជូនឯកសារ',
    subtitle: 'អ្នកប្រើប្រាស់ • អង្គភាព',
    time: '06-មករា-2024 05:49'
  },
  {
    id: 2,
    title: 'បានពិនិត្យឯកសារ',
    subtitle: 'មន្ត្រីពាក់ព័ន្ធ',
    time: '06-មករា-2024 05:57'
  },
  {
    id: 3,
    title: 'កំពុងពិនិត្យ',
    subtitle: 'អង្គភាពពាក់ព័ន្ធ',
    time: '—'
  },
  {
    id: 4,
    title: 'បញ្ចប់ដំណើរការ',
    subtitle: 'អនុម័តឯកសារ',
    time: '—'
  }
]

/* ================= LOGIC ================= */
const stepStatus = (index) => {
  const value = stepsStatus.value[index]
  if (value === 1) return 'green'
  if (value === -1) return 'red'
  return 'yellow'
}

const showComment = computed(() =>
  stepsStatus.value.includes(0) || stepsStatus.value.includes(-1)
)

/* ================= STYLES ================= */
const circleClass = (index) => {
  const s = stepStatus(index)
  if (s === 'green') return 'bg-green-100'
  if (s === 'red') return 'bg-red-100'
  return 'bg-yellow-100'
}

const lineClass = (index) => {
  const s = stepStatus(index)
  if (s === 'green') return 'border-green-300'
  if (s === 'red') return 'border-red-300'
  return 'border-yellow-300'
}

const textClass = (index) => {
  const s = stepStatus(index)
  if (s === 'green') return 'text-green-600'
  if (s === 'red') return 'text-red-600'
  return 'text-yellow-600'
}
</script>
