<script setup>
defineProps({
  documents: {
    type: Array,
    required: true
  }
})

const statusClass = (status) => {
  return {
    pending: 'bg-yellow-400 text-yellow-900',
    approved: 'bg-green-500 text-white',
    rejected: 'bg-red-500 text-white',
    draft: 'bg-gray-400 text-white'
  }[status]
}

const statusText = (status) => {
  return {
    pending: 'កំពុងដំណើរការ',
    approved: 'បានអនុម័ត',
    rejected: 'បដិសេធ',
    draft: 'ព្រាង'
  }[status]
}
</script>

<template>
  <!-- spacing from filter bar -->
  <div class="mt-6">
    <div
      class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 xl:grid-cols-5 gap-6"
    >
      <div
        v-for="doc in documents"
        :key="doc.id"
        class="bg-[var(--ocm-app-bg)] border border-[var(--ocm-app-border)]
               rounded-xl overflow-hidden hover:shadow-md transition"
      >
        <!-- PREVIEW -->
        <div
          class="relative bg-gray-100 h-56 flex items-center justify-center"
        >
          <!-- Status badge -->
          <span
            class="absolute top-3 left-3 text-xs font-semibold px-3 py-1 rounded-full"
            :class="statusClass(doc.status)"
          >
            {{ statusText(doc.status) }}
          </span>

          <!-- Menu -->
          <button
            class="absolute top-3 right-3 text-gray-500 hover:text-gray-800"
          >
            ⋮
          </button>

          <!-- PDF preview -->
          <img
            src="/src/assets/pdf-preview3.png"
            alt="preview"
            class="h-full object-contain p-4"
          />
        </div>

        <!-- CONTENT -->
        <div class="p-4 space-y-3">
          <!-- Title -->
          <div class="flex items-start gap-2">
            <span
              class="w-8 h-8 flex items-center justify-center rounded-lg
                     bg-red-100 text-red-600 font-bold text-xs"
            >
              PDF
            </span>

            <p class="text-sm font-semibold line-clamp-2">
              {{ doc.title }}
            </p>
          </div>

          <!-- Creator -->
          <div class="flex items-center gap-2 text-sm">
            <img
              :src="doc.creatorAvatar"
              class="w-7 h-7 rounded-full object-cover"
            />
            <span class="text-blue-600 font-medium truncate">
              {{ doc.creator }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
