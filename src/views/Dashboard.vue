<template>
  <div class="app_wrap">
    <input type="text" value-model="officer.id" style="border: 1px solid #CCC; " >
  <!-- <Header />
  <DashboardGrid /> -->
  </div>
</template>

<script >
import Header from '@/components/Header.vue'
import DashboardGrid from "../components/DashboardGrid.vue"
import { ref } from 'vue'
import { useStore } from 'vuex'
  export default {
    setup() {
      const store = useStore()

      const officer = ref( null )

      store.dispatch('officer/list').then( res => {
        officer.value = res.data.records[0]
      })
      store.commit('officer/setRecords')

      store.getters['officer/getRecords']
      return {
        officer
      }
    }
  }
</script>
