<template>
  <!-- TOP HEADER -->
  <Header title="លំហូរឯកសារទីស្តីការគណៈរដ្ឋមន្ត្រី" />

  <section class="appppw">
    <div class="flex h-[calc(100vh-64px)] overflow-hidden">
      <!-- SIDEBAR -->
      <Aside />

      <!-- MAIN CONTENT WRAPPER (KEEP sw) -->
      <div class="sw flex flex-col flex-1 overflow-hidden">
        <div class="app_content flex flex-col flex-1 overflow-hidden">

          <!-- PAGE TITLE -->
          
          
          <!-- PDF + TOOLS -->
          <div class="flex flex-1 overflow-hidden doc_details">
            <!-- LEFT : PDF -->
            <div class="flex-1 overflow-hidden">
              <div class="ocm_cwr ">
            <h2 class="h doc-heading t-lspace">សេចក្តីណែនាំ ស្តីពី របៀបរបបនៃការរៀបចំកំណត់បង្ហាញរបស់ទីស្តីការគណៈរដ្ឋមន្ត្រី លើសំណើនិងរបាយការណ៍របស់ក្រសួង ស្ថាប័ន</h2>
          </div>
              <PdfViewer
                src="/docs/report2.pdf"
                class="doc_preview"
              />
              <!-- <PdfViewer
                src="https://snippet.embedpdf.com/ebook.pdf"
                class="w-full h-full"
              /> -->
            </div>

            <!-- RIGHT : WORKFLOW / TIMELINE -->
            <div
              class="w-90 overflow-y-auto doc_sidebar"
            >
              <DocumentTimeline />
            </div>
          </div>

        </div>

        <!-- FOOTER -->
      </div>
    </div>
  </section>
</template>


<script setup>
import Header from '@/components/Header.vue'
import Aside from '@/components/Aside.vue'
import Footer from '@/components/Footer.vue'
import PdfViewer from '@/components/PdfViewer.vue'
import DocumentTimeline from '@/components/DocumentTimeline.vue'
</script>
