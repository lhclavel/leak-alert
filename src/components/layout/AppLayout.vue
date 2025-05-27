<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import AppHeader from './AppHeader.vue'

// Theme state
const currentTab = ref('home')
const router = useRouter()

const setActiveTab = (tab) => {
  currentTab.value = tab
  if (tab === 'home') {
    router.push('/dashboard')
  } else if (tab === 'notifications') {
    router.push('/notifications')
  } else if (tab === 'settings') {
    router.push('/settings')
  }
}
</script>

<template>
  <v-responsive>
    <v-app>
      <AppHeader></AppHeader>
      <v-main>
        <v-container>
          <slot name="content"></slot>
        </v-container>
      </v-main>

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
          class="nav-btn"
          :class="{ active: currentTab === 'notifications' }"
          @click="setActiveTab('notifications')"
        >
          <v-icon class="nav-notifications">mdi-bell</v-icon>
        </button>

        <button
          class="nav-btn"
          :class="{ active: currentTab === 'settings' }"
          @click="setActiveTab('settings')"
        >
          <v-icon class="nav-settings">mdi-cog</v-icon>
        </button>
      </div>
    </v-app>
  </v-responsive>
</template>

<style scoped>
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  display: flex;
  background: #2196f3;
  height: 70px;
  border-top: 1px solid #e0e0e0;
  z-index: 1000;
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

/* Add padding to main content to prevent overlap with fixed bottom nav */
.v-main {
  padding-bottom: 70px !important;
}
</style>
