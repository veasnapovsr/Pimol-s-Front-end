<script setup>
const props = defineProps({
  modelValue: {
    type: String,
    default: 'row' // row | grid
  }
})

const emit = defineEmits(['update:modelValue'])

const setView = (view) => {
  emit('update:modelValue', view)
}
</script>

<template>
  <div class="flex items-center gap-2">
    <!-- Row -->
    <button
      @click="setView('row')"
      :class="[
        'p-2 rounded-lg border transition',
        modelValue === 'row'
          ? 'bg-gray-900 text-white border-gray-900'
          : 'bg-white text-gray-600 hover:bg-gray-100'
      ]"
      title="Row view"
    >
      <!-- row icon -->
      <svg class="w-5 h-5" viewBox="0 0 24 24" fill="none">
        <path d="M4 6h16M4 12h16M4 18h16"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"/>
      </svg>
    </button>

    <!-- Grid -->
    <button
      @click="setView('grid')"
      :class="[
        'p-2 rounded-lg border transition',
        modelValue === 'grid'
          ? 'bg-gray-900 text-white border-gray-900'
          : 'bg-white text-gray-600 hover:bg-gray-100'
      ]"
      title="Grid view"
    >
      <!-- grid icon -->
      <svg class="w-5 h-5" viewBox="0 0 24 24" fill="none">
        <rect x="4" y="4" width="7" height="7" rx="1" stroke="currentColor" stroke-width="2"/>
        <rect x="13" y="4" width="7" height="7" rx="1" stroke="currentColor" stroke-width="2"/>
        <rect x="4" y="13" width="7" height="7" rx="1" stroke="currentColor" stroke-width="2"/>
        <rect x="13" y="13" width="7" height="7" rx="1" stroke="currentColor" stroke-width="2"/>
      </svg>
    </button>
  </div>
</template>
