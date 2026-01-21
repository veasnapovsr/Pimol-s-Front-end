<template>
  <Header title="លំហូរឯកសារទីស្តីការគណៈរដ្ឋមន្ត្រី" />
  <section class="appppw">
    <Aside />
    <div class="sw">
      <div class="flex flex-col gap-4">

        <h1 class="text-2xl">បណ្ណសារឯកសារ</h1>

        <CountNumber />

        <!-- Log activity chart -->
        <LogActivityLineChart />

        <!-- Optional -->
        <!-- <FolderCompo /> -->
        <!-- <DocumentTable /> -->

      </div>

      <Footer />
    </div>
  </section>
</template>


<script setup>
import Header from '@/components/Header.vue'
import Aside from '@/components/Aside.vue'
import Footer from '@/components/Footer.vue'
import FolderCompo from '@/components/History/FolderCompo.vue';
import DocumentTable from '@/components/History/DocumentTable.vue';
import CountNumber from '@/components/CountNumber.vue';
import LogActivityLineChart from '@/components/LogActivityLineChart.vue'
</script>