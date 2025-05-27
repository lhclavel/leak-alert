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
  <AppLayout>
    <template #content>
      <v-container class="pa-4">
        <h2 class="mb-6">Settings</h2>

        <!-- Notifications Card -->
        <v-card class="mb-6 settings-card" elevation="0">
          <v-card-text>
            <div class="d-flex align-center mb-4">
              <v-icon color="primary" size="24" class="mr-3">mdi-bell-outline</v-icon>
              <span class="text-subtitle-1">Notifications</span>
            </div>

            <div class="setting-item mb-4">
              <div class="d-flex align-center justify-space-between">
                <div>
                  <div class="text-body-1 mb-1">Push Notifications</div>
                  <div class="text-caption text-medium-emphasis">
                    Get instant alerts on your device
                  </div>
                </div>
                <v-switch
                  v-model="notifications"
                  color="primary"
                  hide-details
                  @change="saveSettings"
                ></v-switch>
              </div>
            </div>

            <div class="setting-item">
              <div class="d-flex align-center justify-space-between">
                <div>
                  <div class="text-body-1 mb-1">Email Notifications</div>
                  <div class="text-caption text-medium-emphasis">Receive updates in your inbox</div>
                </div>
                <v-switch
                  v-model="emailNotifications"
                  color="primary"
                  hide-details
                  @change="saveSettings"
                ></v-switch>
              </div>
            </div>
          </v-card-text>
        </v-card>

        <!-- About Card -->
        <v-card class="settings-card" elevation="0">
          <v-card-text>
            <div class="d-flex align-center mb-4">
              <v-icon color="primary" size="24" class="mr-3">mdi-information-outline</v-icon>
              <span class="text-subtitle-1">About</span>
            </div>

            <div class="setting-item mb-4">
              <div class="text-body-1 mb-1">Version</div>
              <div class="text-caption text-medium-emphasis">1.0.0</div>
            </div>

            <div class="setting-item">
              <div class="text-body-1 mb-1">Copyright</div>
              <div class="text-caption text-medium-emphasis">© 2025 LeakAlert</div>
            </div>
          </v-card-text>
        </v-card>
      </v-container>
    </template>
  </AppLayout>
</template>

<style scoped>
.settings-card {
  background-color: #f8fafc !important;
  border-radius: 16px !important;
  border: 1px solid #e2e8f0 !important;
}

.setting-item {
  padding: 12px 0;
}

:deep(.v-switch) {
  .v-switch__track {
    opacity: 0.2;
  }

  .v-switch__thumb {
    box-shadow: none;
  }
}

:deep(.v-switch--active) {
  .v-switch__track {
    opacity: 0.3;
  }
}

/* Update Vuetify theme colors in your main.js or theme configuration */
/*
{
  primary: '#2196f3', // Sky blue
}
*/
</style>
