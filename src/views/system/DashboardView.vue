<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import AppLayout from '@/components/layout/AppLayout.vue'
import CreateView from '@/views/system/CreateView.vue'

// Dashboard state
const leakStatus = ref('No leaks detected')
const lastUpdate = ref('2 mins ago')
const batteryLevel = ref(85)

const router = useRouter()

const showCreateButton = ref(false)

const toggleCreateButton = () => {
  showCreateButton.value = !showCreateButton.value
}

const handleCreate = () => {
  router.push('/create')
  showCreateButton.value = false
}
</script>

<template>
  <AppLayout>
    <template #content>
      <div class="dashboard-container">
        <!-- Header -->

        <!-- Main Content -->
        <div class="main-content">
          <!-- Logo Section -->
          <div class="logo-section">
            <div class="logo-container">
              <img src="/images/logo1.png" alt="LeakAlert Logo" class="logo-image" />
            </div>
            <h1 class="welcome-text">Welcome to LeakAlert!</h1>
          </div>

          <!-- Status Card -->
          <div class="status-card">
            <div class="card-content">
              <!-- Status Text -->
              <h3 class="status-text">{{ leakStatus }}</h3>
              <p class="last-update">Last updated: {{ lastUpdate }}</p>

              <!-- Quick Stats -->
              <div class="quick-stats">
                <div class="stat-item">
                  <span class="battery-icon">🔋</span>
                  <span class="stat-text">{{ batteryLevel }}%</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <button
        class="floating-add-btn"
        :class="{ active: showCreateButton }"
        @click="toggleCreateButton"
      >
        <div class="add-button">
          <span class="nav-icon" :class="{ rotated: showCreateButton }">+</span>
        </div>

        <!-- Create Button Popup -->
        <div class="create-popup" :class="{ visible: showCreateButton }" @click.stop="handleCreate">
          <span class="create-text">Create</span>
        </div>
      </button>
    </template>
  </AppLayout>
</template>

<style scoped>
.dashboard-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f5f5f5;
  font-family: Arial, sans-serif;
}

.main-content {
  flex: 1;
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

.status-card {
  width: 100%;
  max-width: 400px;
  background: white;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin-top: 16px;
}

.card-content {
  padding: 32px;
  text-align: center;
}

.logo-section {
  text-align: center;
  margin-bottom: 16px;
}

.logo-container {
  margin-top: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 24px;
}

.logo-image {
  width: 250px;
  height: 250px;
  max-width: 400px;
  object-fit: contain;
}

.status-text {
  color: #333;
  font-weight: 500;
  font-size: 1.1rem;
  margin: 16px 0 8px 0;
}

.last-update {
  color: #666;
  font-size: 0.9rem;
  margin: 0 0 24px 0;
}

.quick-stats {
  display: flex;
  justify-content: center;
  gap: 16px;
}

.stat-item {
  display: flex;
  align-items: center;
  background: #f8f9fa;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.9rem;
  color: #666;
}

.battery-icon {
  margin-right: 8px;
  font-size: 1rem;
}

.stat-text {
  font-weight: 500;
}

.floating-add-btn {
  position: fixed;
  bottom: 90px;
  right: 20px;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 1000;
}

.add-button {
  background: #2196f3;
  border-radius: 50%;
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition:
    transform 0.2s ease,
    background-color 0.2s ease;
}

.floating-add-btn:hover .add-button {
  transform: scale(1.1);
  background: #1976d2;
}

.nav-icon {
  font-size: 28px;
  color: white;
  transition: transform 0.2s ease;
}

.nav-icon.rotated {
  transform: rotate(45deg);
}

.create-popup {
  position: absolute;
  bottom: 100%;
  right: 0;
  transform: translateY(-10px);
  background: #1976d2;
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 14px;
  font-weight: 500;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  margin-bottom: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.create-popup.visible {
  opacity: 1;
  visibility: visible;
  transform: translateY(-5px);
}

.create-popup:hover {
  background: #1565c0;
  transform: translateY(-8px);
}
</style>
