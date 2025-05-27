<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import AppLayout from '@/components/layout/AppLayout.vue'
import CreateView from '@/views/system/CreateView.vue'

// Dashboard state
const leakStatus = ref('Leaks detected')
const lastUpdate = ref('10 mins ago')

const router = useRouter()

const showCreateButton = ref(false)

const toggleCreateButton = () => {
  showCreateButton.value = !showCreateButton.value
}

const handleCreate = () => {
  router.push('/create')
  showCreateButton.value = false
}

const leaks = ref([
  {
    id: 1,
    location: 'Kitchen Sink',
    severity: 'Minor',
    time: '10 mins ago',
    status: 'active',
  },
  {
    id: 2,
    location: 'Bathroom Pipe',
    severity: 'Major',
    time: '1 hour ago',
    status: 'pending',
  },
  {
    id: 3,
    location: 'Garden Sprinkler',
    severity: 'Minor',
    time: '2 hours ago',
    status: 'active',
  },
  {
    id: 4,
    location: 'Basement Pipeline',
    severity: 'Major',
    time: '3 hours ago',
    status: 'active',
  },
  {
    id: 5,
    location: 'Outdoor Faucet',
    severity: 'Minor',
    time: '4 hours ago',
    status: 'pending',
  },
])
</script>

<template>
  <AppLayout>
    <template #content>
      <div class="dashboard-container">
        <div class="main-content">
          <!-- Logo Section -->
          <div class="logo-section">
            <div class="logo-container">
              <img src="/images/logo1.png" alt="LeakAlert Logo" class="logo-image" />
            </div>
            <h1 class="text-h5 text-primary font-weight-medium mb-2">Welcome to LeakAlert!</h1>
            <p class="text-subtitle- text-medium-emphasis">
              Monitor your water system in real-time
            </p>
          </div>

          <!-- Status Card -->
          <div class="status-card">
            <div class="card-header">
              <div>
                <h3 class="text-h6 text-primary mb-1">{{ leakStatus }}</h3>
                <p class="text-caption text-medium-emphasis">Last updated: {{ lastUpdate }}</p>
              </div>
              <v-chip color="primary" variant="flat" size="small">Live</v-chip>
            </div>

            <!-- Leak List -->
            <div class="leak-list">
              <div v-for="leak in leaks" :key="leak.id" class="leak-item">
                <div class="leak-content">
                  <div class="leak-icon" :class="leak.severity.toLowerCase()">
                    <v-icon size="20">
                      {{ leak.severity === 'Minor' ? 'mdi-alert' : 'mdi-alert-circle' }}
                    </v-icon>
                  </div>
                  <div class="leak-info">
                    <div class="d-flex align-center justify-space-between mb-1">
                      <span class="text-subtitle-2 font-weight-medium">{{ leak.location }}</span>
                      <span class="text-caption text-medium-emphasis">{{ leak.time }}</span>
                    </div>
                    <v-chip
                      size="x-small"
                      :color="leak.severity === 'Minor' ? 'warning' : 'error'"
                      variant="tonal"
                      class="leak-severity"
                    >
                      {{ leak.severity }}
                    </v-chip>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Floating Action Button -->
        <button
          class="floating-add-btn"
          :class="{ active: showCreateButton }"
          @click="toggleCreateButton"
        >
          <div class="add-button">
            <v-icon>{{ showCreateButton ? 'mdi-close' : 'mdi-plus' }}</v-icon>
          </div>
        </button>
      </div>
    </template>
  </AppLayout>
</template>

<style scoped>
.dashboard-container {
  min-height: 100vh;
  background-color: #f8fafc;
  padding-bottom: 80px;
}

.main-content {
  max-width: 600px;
  margin: 0 auto;
  padding: 24px 16px;
  padding-bottom: 100px; /* Add space for the floating button */
}

.logo-section {
  text-align: center;
  margin-bottom: 32px;
}

.logo-image {
  width: 140px;
  height: 140px;
  margin-bottom: 24px;
}

.status-card {
  background: white;
  border-radius: 16px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  overflow: hidden;
}

.card-header {
  padding: 20px 24px;
  border-bottom: 1px solid #f1f1f1;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.leak-list {
  padding: 16px;
  max-height: 300px; /* Limit height to prevent overlap */
  overflow-y: auto;
  scrollbar-width: thin;
}

/* Custom scrollbar styling */
.leak-list::-webkit-scrollbar {
  width: 6px;
}

.leak-list::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 3px;
}

.leak-list::-webkit-scrollbar-thumb {
  background: #c1c1c1;
  border-radius: 3px;
}

.leak-list::-webkit-scrollbar-thumb:hover {
  background: #a1a1a1;
}

.leak-item {
  padding: 12px;
  border-radius: 12px;
  transition: background-color 0.2s ease;
}

.leak-item:hover {
  background-color: #f8fafc;
}

.leak-content {
  display: flex;
  align-items: flex-start;
  gap: 16px;
}

.leak-icon {
  width: 32px;
  height: 32px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.leak-icon.minor {
  background: #fff3e0;
  color: #f57c00;
}

.leak-icon.major {
  background: #ffebee;
  color: #d32f2f;
}

.leak-info {
  flex: 1;
}

.leak-severity {
  font-size: 11px !important;
}

.floating-add-btn {
  position: fixed;
  bottom: 90px;
  right: 20px;
  z-index: 1000;
  border: none;
  background: none;
  cursor: pointer;
}

.add-button {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  background: #2196f3;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(33, 150, 243, 0.25);
  transition: all 0.2s ease;
}

.add-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(33, 150, 243, 0.3);
}
</style>
