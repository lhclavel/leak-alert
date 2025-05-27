<script setup>
import { ref } from 'vue'
import AppLayout from '@/components/layout/AppLayout.vue'

const notifications = ref([
  {
    id: 1,
    title: 'Water Leak Detected',
    message: 'High water usage detected in Kitchen area',
    time: '2 mins ago',
    isUnread: true,
    type: 'warning',
  },
  {
    id: 2,
    title: 'Monthly Report',
    message: 'Your water consumption report is ready',
    time: '1 hour ago',
    isUnread: false,
    type: 'info',
  },
  {
    id: 3,
    title: 'System Update',
    message: 'LeakAlert system has been updated',
    time: '1 day ago',
    isUnread: false,
    type: 'success',
  },
  {
    id: 4,
    title: 'Critical Leak Alert',
    message: 'Major leak detected in Bathroom pipe, immediate action required',
    time: '5 mins ago',
    isUnread: true,
    type: 'warning',
  },

  {
    id: 5,
    title: 'Maintenance Reminder',
    message: 'Scheduled maintenance check due in 2 days',
    time: '3 hours ago',
    isUnread: false,
    type: 'info',
  },
  {
    id: 6,
    title: 'Sensor Calibrated',
    message: 'Water flow sensor has been successfully calibrated',
    time: '2 days ago',
    isUnread: false,
    type: 'success',
  },
])

const markAsRead = (id) => {
  const notification = notifications.value.find((n) => n.id === id)
  if (notification) {
    notification.isUnread = false
  }
}
</script>

<template>
  <AppLayout>
    <template #content>
      <v-container class="notifications-container">
        <!-- Header Section -->
        <div class="header-section mb-6">
          <h2 class="text-subtitle-4">Notifications</h2>
          <p class="text-subtitle-2 text-medium-emphasis mt-1">
            Stay updated with your leak alerts
          </p>
        </div>

        <!-- Notifications List -->
        <v-list v-if="notifications.length" class="notifications-list">
          <v-list-item
            v-for="notification in notifications"
            :key="notification.id"
            :class="{ unread: notification.isUnread }"
            @click="markAsRead(notification.id)"
            class="notification-item"
          >
            <template v-slot:prepend>
              <div :class="['notification-icon', notification.type]">
                <v-icon size="20" color="white">
                  {{
                    notification.type === 'warning'
                      ? 'mdi-alert'
                      : notification.type === 'info'
                        ? 'mdi-information'
                        : 'mdi-check'
                  }}
                </v-icon>
              </div>
            </template>

            <v-list-item-title
              class="text-subtitle-1 font-weight-medium mb-1"
              :class="{ 'text-primary': notification.isUnread }"
            >
              {{ notification.title }}
            </v-list-item-title>

            <v-list-item-subtitle class="text-body-2 text-medium-emphasis">
              {{ notification.message }}
            </v-list-item-subtitle>

            <template v-slot:append>
              <div class="d-flex flex-column align-end">
                <span class="text-caption text-medium-emphasis">{{ notification.time }}</span>
                <v-icon v-if="notification.isUnread" color="primary" size="8" class="mt-2"
                  >mdi-circle</v-icon
                >
              </div>
            </template>
          </v-list-item>
        </v-list>

        <!-- Empty State -->
        <div v-else class="empty-state">
          <v-icon size="64" color="grey-lighten-2">mdi-bell-sleep</v-icon>
          <p class="text-body-1 text-medium-emphasis mt-4">All caught up!</p>
          <p class="text-caption text-medium-emphasis">No new notifications</p>
        </div>
      </v-container>
    </template>
  </AppLayout>
</template>

<style scoped>
.notifications-container {
  max-width: 600px;
  margin: 0 auto;
  padding-bottom: 70px;
}

.notifications-list {
  background: transparent !important;
}

.notification-item {
  background: white;
  margin-bottom: 25px;
  border-radius: 12px !important;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  transition: all 0.2s ease;
}

.notification-item:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.notification-item.unread {
  background: #f8faff;
}

.notification-icon {
  width: 32px;
  height: 32px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 12px;
}

.notification-icon.warning {
  background: #ff9800;
}

.notification-icon.info {
  background: #2196f3;
}

.notification-icon.success {
  background: #4caf50;
}

.empty-state {
  text-align: center;
  padding: 64px 0;
  background: white;
  border-radius: 16px;
  margin-top: 16px;
}

/* Custom scrollbar for better aesthetics */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb {
  background: #d1d1d1;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #b1b1b1;
}
</style>
