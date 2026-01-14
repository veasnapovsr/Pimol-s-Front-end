<template>
  <!-- TOP HEADER -->
  <Header />

  <section class="appppw">
    <!-- SIDEBAR -->
    <Aside />

    <!-- MAIN CONTENT WRAPPER -->
    <div class="sw">
      <div class="app_content">

        <!-- PAGE TITLE -->
        <div class="ocm_cwr">
          <h2 class="h wttt t-lspace">ឯកសារ PDF</h2>
        </div>

        <!-- ===== MAIN GRID ===== -->
        <div class="ocm_card_wr">
          <div
            class="ocm_card_content p-4
                   h-[calc(100vh-220px)]
                   grid grid-cols-12 gap-4"
          >

            <!-- ===== LEFT : PDF VIEWER ===== -->
            <div class="col-span-8 h-full overflow-hidden rounded-lg border">
              <PdfViewer src="/public/docs/reportMenu.pdf" />
            </div>

            <!-- ===== RIGHT : WORKFLOW / TIMELINE ===== -->
            <div
              class="col-span-4 h-full overflow-y-auto
                     rounded-lg border bg-white p-4"
            >
              <DocumentTimeline />
            </div>

          </div>
        </div>

      </div>

      <!-- FOOTER -->
      <Footer />
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
