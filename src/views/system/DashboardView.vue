<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router' // Import Vue Router
import AppHeader from '@/components/layout/AppHeader.vue'

// Dashboard state
const currentTab = ref('home')
const showCreateButton = ref(false)
const router = useRouter()

const setActiveTab = (tab) => {
  currentTab.value = tab
  if (tab === 'settings') {
    router.push('/settings') // Navigate to the SettingsView
  }
}

// Add button functionality
const toggleCreateButton = () => {
  showCreateButton.value = !showCreateButton.value
}

const handleCreate = () => {
  // Navigate to CreateView
  router.push('/create') // Replace '/create' with the actual route path for CreateView
  showCreateButton.value = false
}
</script>

<template>
  <div class="dashboard-container">
    <!-- Header -->
    <AppHeader />

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

    <!-- Bottom Navigation -->
    <div class="bottom-nav">
      <button
        class="nav-btn"
        :class="{ active: currentTab === 'home' }"
        @click="setActiveTab('home')"
      >
        <v-icon class="nav-home">mdi-home</v-icon>
      </button>

      <button
        class="nav-btn add-btn"
        :class="{ active: currentTab === 'add' }"
        @click="toggleCreateButton"
      >
        <div class="add-button">
          <span class="nav-icon" :class="{ rotated: showCreateButton }">+</span>
        </div>

        <!-- Create Button Popup -->
        <div
          class="create-popup my-1"
          :class="{ visible: showCreateButton }"
          @click.stop="handleCreate"
        >
          <span class="create-text">Create</span>
        </div>
      </button>

      <button
        class="nav-btn"
        :class="{ active: currentTab === 'settings' }"
        @click="setActiveTab('settings')"
      >
        <v-icon class="nav-settings">mdi-cog</v-icon>
      </button>
    </div>
  </div>
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
  justify-content: flex-start; /* Align content to the top */
}

.status-card {
  width: 100%;
  max-width: 400px;
  background: white;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin-top: 16px; /* Add spacing between the welcome text and the card */
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

.bottom-nav {
  display: flex;
  background: #2196f3;
  height: 70px;
  border-top: 1px solid #e0e0e0;
}

.nav-btn {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: none;
  border: none;
  color: rgba(255, 255, 255, 0.7);
  cursor: pointer;
  transition: color 0.3s ease;
  padding: 8px;
}

.nav-btn:hover,
.nav-btn.active {
  color: white;
}

.nav-icon {
  font-size: 20px;
  margin-bottom: 4px;
}

.nav-home {
  max-width: 10%;
}

.add-btn {
  position: relative;
}

.add-button {
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(10px);
  transition:
    transform 0.2s ease,
    background-color 0.2s ease;
}

.add-btn:hover .add-button {
  transform: scale(1.1);
  background: rgba(255, 255, 255, 0.3);
}

.add-button .nav-icon {
  font-size: 24px;
  color: white;
  margin-bottom: 0;
  transition: transform 0.2s ease;
}

.nav-icon.rotated {
  transform: rotate(45deg);
}

.add-btn:hover .nav-icon:not(.rotated) {
  transform: rotate(90deg);
}

/* Create Button Popup */
.create-popup {
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%) translateY(-10px);
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
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  z-index: 10;
}

.create-popup::after {
  content: '';
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-top: 6px solid #1976d2;
}

.create-popup.visible {
  opacity: 1;
  visibility: visible;
  transform: translateX(-50%) translateY(-5px);
}

.create-popup:hover {
  background: #1565c0;
  transform: translateX(-50%) translateY(-8px) scale(1.05);
}

.create-text {
  display: block;
}
</style>
