<script setup>
import { ref } from 'vue'

const isSidebarOpen = ref(false)

// Toggle sidebar menu
function toggleSidebar() {
  isSidebarOpen.value = !isSidebarOpen.value
}

// Handle logout
function logout() {
  window.location.href = '/login'
}
</script>

<template>
  <header class="app-header">
    <div class="header-left"><span class="leak">Leak</span><span class="alert">Alert</span></div>
    <div class="menu-container">
      <button class="menu-btn" @click="toggleSidebar" aria-label="Menu">☰</button>
      <!-- Sidebar menu -->
      <div :class="['sidebar', { 'sidebar-open': isSidebarOpen }]">
        <ul>
          <li>
            <a href="#"> <span class="mdi mdi-account-circle-outline me-2"></span>Profile</a>
          </li>
          <li>
            <a href="#"> <span class="mdi mdi-bell-outline me-2"></span>Notifications</a>
          </li>
          <v-divider class="my-5"></v-divider>
          <li>
            <a href="#" @click.prevent="logout"> <span class="mdi mdi-logout me-2"></span>Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<style scoped>
.app-header {
  background: #2196f3;
  padding: 8px 16px;
  display: flex;
  justify-content: space-between; /* align left and right */
  align-items: center;
  font-size: 1.3rem;
  font-weight: bold;
  color: #fff;
  letter-spacing: 0.5px;
  width: 100%;
  box-sizing: border-box;
  position: relative; /* for sidebar positioning */
}

/* Style for the left content */
.header-left {
  display: flex;
  align-items: center;
}

/* Keep your existing styles for leak and alert */
.leak {
  color: #fff;
}
.alert {
  color: #222;
}

/* Style for the menu button */
.menu-btn {
  background: transparent;
  border: none;
  font-size: 1.5rem;
  color: #000000;
  cursor: pointer;
  position: relative; /* Ensure it stays above the sidebar */
  z-index: 1101; /* Higher than the sidebar */
}

/* Sidebar styles */
.sidebar {
  position: fixed; /* Make it fixed to cover the screen */
  top: 0;
  right: -250px; /* Start off-screen */
  height: 100%; /* Full height */
  width: 250px; /* Adjust width as needed */
  background: #2196f3;
  box-shadow: -2px 0 8px rgba(0, 0, 0, 0.2);
  padding: 50px 0 20px; /* Add padding at the top to push content down */
  z-index: 1000; /* Lower than the menu button */
  border-radius: 0; /* Remove border-radius for full coverage */
  transition: right 0.3s ease; /* Add smooth transition */
}

.sidebar ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.sidebar li {
  padding: 8px 16px; /* Adjust padding for better spacing */
  font-size: 1rem; /* Medium font size for list items */
  margin: 4px 12px; /* Add vertical spacing between items */
  border-radius: 4px; /* Add rounded corners for hover effect */
  display: flex; /* Align icon and text horizontally */
  align-items: center;
}

.sidebar li .mdi {
  margin-right: 8px; /* Add space between the icon and text */
  font-size: 1.5rem; /* Set medium size for icons */
}

.sidebar li:hover {
  background-color: #f0f0f0;
}

.sidebar a {
  text-decoration: none;
  color: #333;
  display: flex; /* Align icon and text horizontally */
  align-items: center;
}
/* Sidebar open state */
.sidebar-open {
  right: 0; /* Slide into view */
}
</style>
