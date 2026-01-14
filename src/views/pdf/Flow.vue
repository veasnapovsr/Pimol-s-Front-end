<script setup>
import { ref, computed } from 'vue'

/* =======================
   LAYOUT COMPONENTS
======================= */
import Header from '@/components/Header.vue'
import Aside from '@/components/Aside.vue'
import Footer from '@/components/Footer.vue'

/* =======================
   FLOW COMPONENTS
======================= */
import FlowStats from '@/components/flow/FlowStatus.vue'
import FlowFilters from '@/components/flow/FlowFilters.vue'
import FlowTable from '@/components/flow/FlowTable.vue'
import FlowGrid from '@/components/flow/FlowGrid.vue'
import RowToGrid from '@/components/flow/RowToGrid.vue'

/* =======================
   FILTER COMPONENTS
======================= */
import DateSelect from '@/components/flow/DateSelect.vue'
import AuthorNameFilter from '@/components/flow/AuthorNameFilter.vue'
import DocumentNameFilter from '@/components/flow/DocumentNameFilter.vue'
import DocumentStatusFilter from '@/components/flow/DocumentStatusFilter.vue'

/* =======================
   DATA
======================= */
import { flowStats } from '@/data/Flowstatuscheck'
import { documents } from '@/data/documents'

/* =======================
   VIEW MODE
======================= */
const viewMode = ref('row') // row | grid

/* =======================
   FILTER STATE
======================= */
const selectedDate = ref('')
const selectedAuthor = ref('')
const selectedName = ref('')
const selectedStatus = ref('')

/* =======================
   FILTER LOGIC (SAFE BASE)
======================= */
const filteredDocuments = computed(() => {
  return documents.filter(doc => {
    const matchName =
      !selectedName.value ||
      doc.title.includes(selectedName.value)

    const matchAuthor =
      !selectedAuthor.value ||
      doc.creator.includes(selectedAuthor.value)

    const matchStatus =
      !selectedStatus.value ||
      doc.status === selectedStatus.value

    const matchDate =
      !selectedDate.value ||
      doc.date === selectedDate.value

    return matchName && matchAuthor && matchStatus && matchDate
  })
})
</script>

<template>
  <!-- TOP HEADER -->
  <Header />

  <section class="appppw">
    <!-- SIDEBAR -->
    <Aside />

    <!-- MAIN CONTENT -->
    <div class="sw">
      <div class="app_content">

        <!-- PAGE TITLE -->
        <div class="ocm_cwr flex items-center justify-between">
          <h2 class="h wttt t-lspace">
            លំហូរឯកសារ
          </h2>

          <!-- ROW / GRID TOGGLE -->
          <RowToGrid v-model="viewMode" />
        </div>

        <!-- STATS -->
        <FlowStats :stats="flowStats" />

        <!-- FILTER BAR -->
        <FlowFilters>
          <div class="ocm_filter_w d-flex align-items-center gap-3 flex-wrap">

            <DocumentNameFilter
              @change="selectedName = $event"
            />

            <DateSelect
              v-model="selectedDate"
            />

            <AuthorNameFilter
              @change="selectedAuthor = $event"
            />

            <DocumentStatusFilter
              @change="selectedStatus = $event"
            />

            <!-- SEARCH BUTTON -->
            <button class="button-primary">
              ស្វែងរក
            </button>

          </div>
        </FlowFilters>

        <!-- CONTENT -->
        <div class="mt-6">

          <!-- ROW VIEW -->
          <FlowTable
            v-if="viewMode === 'row'"
            :documents="filteredDocuments"
          />

          <!-- GRID VIEW -->
          <FlowGrid
            v-else
            :documents="filteredDocuments"
          />

        </div>

      </div>

      <!-- FOOTER -->
      <Footer />
    </div>
  </section>
</template>
