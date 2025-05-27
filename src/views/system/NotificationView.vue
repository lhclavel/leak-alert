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
      <v-container class="notifications-container pa-4">
        <h2 class="font-weight-bold mb-4">Notifications</h2>

        <v-list v-if="notifications.length" class="notifications-list">
          <v-list-item
            v-for="notification in notifications"
            :key="notification.id"
            :class="{ unread: notification.isUnread }"
            @click="markAsRead(notification.id)"
          >
            <template v-slot:prepend>
              <v-icon
                :color="
                  notification.type === 'warning'
                    ? 'warning'
                    : notification.type === 'info'
                      ? 'info'
                      : 'success'
                "
                class="mr-3"
              >
                {{
                  notification.type === 'warning'
                    ? 'mdi-alert-circle'
                    : notification.type === 'info'
                      ? 'mdi-information'
                      : 'mdi-check-circle'
                }}
              </v-icon>
            </template>

            <v-list-item-title
              class="font-weight-medium"
              :class="{ 'text-primary': notification.isUnread }"
            >
              {{ notification.title }}
            </v-list-item-title>

            <v-list-item-subtitle class="mt-1">
              {{ notification.message }}
            </v-list-item-subtitle>

            <template v-slot:append>
              <span class="text-caption text-medium-emphasis">{{ notification.time }}</span>
            </template>
          </v-list-item>
        </v-list>

        <div v-else class="empty-state">
          <v-icon size="64" color="grey-lighten-1">mdi-bell-off</v-icon>
          <p class="text-body-1 text-medium-emphasis mt-4">No notifications yet</p>
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
  border-radius: 8px;
  overflow: hidden;
}

.v-list-item {
  margin-bottom: 8px;
  border-radius: 8px;
  transition: background-color 0.2s ease;
}

.v-list-item.unread {
  background-color: rgb(33, 150, 243, 0.05);
}

.empty-state {
  text-align: center;
  padding: 48px 0;
}

.v-list-item:hover {
  background-color: rgb(33, 150, 243, 0.1);
}
</style>
