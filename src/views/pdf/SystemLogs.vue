<template>
  <Header title="លំហូរឯកសារទីស្តីការគណៈរដ្ឋមន្ត្រី" />

  <section class="appppw">
    <Aside />

    <div class="sw">
      <div class="flex flex-col">

        <!-- Page title -->
        <div class="ocm_cwr flex items-center justify-between">
          <h2 class="h wttt t-lspace">Logs ប្រព័ន្ធគ្រប់គ្រង</h2>
        </div>

        <CountNumber />

        <!-- MAIN GRID -->
        <div class="dashboard-grid">

          <!-- LEFT COLUMN -->
          <div class="dashboard-left">

            <!-- CHART + DOCUMENT VIEW (SAME ROW) -->
            <div class="dashboard-row">

              <!-- Chart -->
              <div class="dashboard-card chart-card">
                <LogActivityLineChart />
              </div>

              <!-- Document Views -->
              <div class="dashboard-card view-card">
                <DocumentViewDonut />
              </div>

            </div>

            <!-- TOP 10 USERS -->
            <div>
              <div class="ocm_cwr mb-4">
                <h3 class="h wttt t-lspace">
                  អ្នកប្រើប្រាស់សកម្មបំផុតចំណាត់ថ្នាក់កំពូលទាំង ១០
                </h3>
              </div>

              <TopActiveUsers :users="topActiveUsers" />
            </div>

          </div>

          <!-- RIGHT COLUMN -->
          <div class="dashboard-right">
            <OnlineUsers />
          </div>

        </div>

      </div>

      <Footer />
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

import Header from '@/components/Header.vue'
import Aside from '@/components/Aside.vue'
import Footer from '@/components/Footer.vue'
import CountNumber from '@/components/CountNumber.vue'
import LogActivityLineChart from '@/components/LogActivityLineChart.vue'
import OnlineUsers from '@/components/OnlineUserList.vue'
import TopActiveUsers from '@/components/TopActiveUsers.vue'
import DocumentViewDonut from '@/components/DocumentViewDonut.vue'

import { leaders } from '@/data/leader'
import { documents } from '@/data/documents'

// Logs
const logs = ref([])

// Mock logs generator
const generateMockLogs = () => {
  const mockLogs = []

  documents.forEach((doc) => {
    const leader = leaders[Math.floor(Math.random() * leaders.length)]

    mockLogs.push({
      userName: doc.creator || leader.name,
      userAvatar:
        doc.creatorAvatar ||
        leader.img ||
        `https://ui-avatars.com/api/?name=${encodeURIComponent(
          doc.creator || leader.name
        )}&background=0031c3&color=fff`
    })
  })

  return mockLogs
}

// Top 10 Active Users
const topActiveUsers = computed(() => {
  const userMap = new Map()

  logs.value.forEach((log) => {
    if (!userMap.has(log.userName)) {
      userMap.set(log.userName, {
        name: log.userName,
        img: log.userAvatar,
        count: 0
      })
    }
    userMap.get(log.userName).count++
  })

  return Array.from(userMap.values())
    .sort((a, b) => b.count - a.count)
    .slice(0, 10)
})

onMounted(() => {
  logs.value = generateMockLogs()
})
</script>

<style scoped>
/* Main grid */
.dashboard-grid {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 20px;
  margin-bottom: 20px;
}

/* Left column */
.dashboard-left {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

/* Chart + View row */
.dashboard-row {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 20px;
}

/* Card */
.dashboard-card {
  background: white;
  border-radius: 16px;
  padding: 20px;
  box-shadow: 0 12px 30px rgba(15, 23, 42, 0.05);
}

/* Chart sizing */
.chart-card {
  min-height: 320px;
}

/* View card center */
.view-card {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Right column */
.dashboard-right {
  position: sticky;
  top: 20px;
  height: fit-content;
}

/* Responsive */
@media (max-width: 1024px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
  }

  .dashboard-row {
    grid-template-columns: 1fr;
  }

  .dashboard-right {
    position: relative;
  }
}
</style>
