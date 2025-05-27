<script setup>
import { ref, onMounted } from 'vue'
import { useTheme } from 'vuetify'
import { useRouter } from 'vue-router'
import AppLayout from '@/components/layout/AppLayout.vue'
import AppHeader from '@/components/layout/AppHeader.vue'

const notifications = ref(true)
const emailNotifications = ref(true)
const loading = ref(false)

const currentTab = ref('settings')
const showCreateButton = ref(false)

const router = useRouter() // Initialize the router instance

const saveSettings = () => {
  loading.value = true
  try {
    // Save settings to localStorage
    localStorage.setItem('notifications', notifications.value)
    localStorage.setItem('emailNotifications', emailNotifications.value)
  } finally {
    loading.value = false
  }
}

const setActiveTab = (tab) => {
  currentTab.value = tab
  if (tab === 'home') {
    router.push('/dashboard') // Navigate to DashboardView
  } else if (tab === 'settings') {
    router.push('/settings') // Navigate to SettingsView
  }
}

const toggleCreateButton = () => {
  showCreateButton.value = !showCreateButton.value
}

const handleCreate = () => {
  router.push('/create') // Navigate to CreateView
  showCreateButton.value = false
}
</script>

<template>
  <v-app>
    <app-header title="CCIS Portal" />
    <v-main>
      <v-container fluid class="py-6">
        <v-row>
          <v-col>
            <h2 class="font-weight-bold mb-1">Settings</h2>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="12" md="8" lg="6">
            <v-card class="mb-4">
              <v-card-title class="text-h6">Notifications</v-card-title>
              <v-divider />
              <v-card-text>
                <v-list>
                  <v-list-item>
                    <template v-slot:prepend>
                      <v-icon>mdi-bell</v-icon>
                    </template>
                    <v-list-item-title>Push Notifications</v-list-item-title>
                    <template v-slot:append>
                      <v-switch
                        v-model="notifications"
                        color="blue-darken-3"
                        @change="saveSettings"
                      />
                    </template>
                  </v-list-item>
                  <v-list-item>
                    <template v-slot:prepend>
                      <v-icon>mdi-email</v-icon>
                    </template>
                    <v-list-item-title>Email Notifications</v-list-item-title>
                    <template v-slot:append>
                      <v-switch
                        v-model="emailNotifications"
                        color="blue-darken-3"
                        @change="saveSettings"
                      />
                    </template>
                  </v-list-item>
                </v-list>
              </v-card-text>
            </v-card>

            <v-card>
              <v-card-title class="text-h6">About</v-card-title>
              <v-divider />
              <v-card-text>
                <v-list>
                  <v-list-item>
                    <template v-slot:prepend>
                      <v-icon>mdi-information</v-icon>
                    </template>
                    <v-list-item-title>Version</v-list-item-title>
                    <v-list-item-subtitle>1.0.0</v-list-item-subtitle>
                  </v-list-item>
                  <v-list-item>
                    <template v-slot:prepend>
                      <v-icon>mdi-copyright</v-icon>
                    </template>
                    <v-list-item-title>Copyright</v-list-item-title>
                    <v-list-item-subtitle>© 2025 LeakAlert</v-list-item-subtitle>
                  </v-list-item>
                </v-list>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
  <AppLayout />
</template>

<style scoped>
.v-card {
  border-radius: 12px;
  overflow: hidden;
}

.v-list-item {
  min-height: 48px;
}

/* Bottom Navigation */
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
