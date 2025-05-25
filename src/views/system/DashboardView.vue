<script setup>
import { ref } from 'vue'
import AppHeader from '@/components/layout/AppHeader.vue'

// Dashboard state
const currentTab = ref('home')

// Sample data - you can replace with real data
const leakStatus = ref('No leaks detected')
const batteryLevel = ref(85)
const lastUpdate = ref('2 minutes ago')

// Tab switching function
const setActiveTab = (tab) => {
  currentTab.value = tab
}
</script>

<template>
  <div class="dashboard-container">
    <!-- Header -->
    <AppHeader />

    <!-- Main Content -->
    <div class="main-content">
      <!-- Status Card -->
      <div class="status-card">
        <div class="card-content">
          <!-- Logo -->
          <div class="logo-container">
            <img src="/images/logo1.png" alt="LeakAlert Logo" class="logo-image" />
          </div>

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
        @click="setActiveTab('add')"
      >
        <div class="add-button">
          <span class="nav-icon">+</span>
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
  align-items: center;
  justify-content: center;
}

.status-card {
  width: 100%;
  max-width: 400px;
  background: white;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.card-content {
  padding: 32px;
  text-align: center;
}

.logo-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 24px;
}

.logo-image {
  width: 120px;
  height: 120px;
  max-width: 120px;
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
}

.add-button .nav-icon {
  font-size: 24px;
  color: white;
  margin-bottom: 0;
}

/* Mobile responsiveness */
@media (max-width: 600px) {
  .main-content {
    padding: 12px;
  }

  .logo-image {
    width: 100px;
    height: 100px;
  }

  .status-text {
    font-size: 1rem;
  }

  .card-content {
    padding: 24px;
  }
}
</style>
