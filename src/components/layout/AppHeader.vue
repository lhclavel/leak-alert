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
      <div v-if="isSidebarOpen" class="sidebar">
        <ul>
          <li><a href="#">Profile</a></li>
          <li><a href="#">Notifications</a></li>
          <!-- Updated Logout link -->
          <li><a href="#" @click.prevent="logout">Logout</a></li>
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
  color: #fff;
  cursor: pointer;
}

/* Sidebar styles */
.sidebar {
  position: absolute;
  top: 100%;
  right: 16px; /* align with header padding */
  width: 160px;
  background: #fff;
  border: 1px solid #ccc;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  padding: 10px 0;
  z-index: 1000;
  border-radius: 4px;
}

.sidebar ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.sidebar li {
  padding: 10px 20px;
  font-size: 1rem; /* medium font size for list items */
}

.sidebar li:hover {
  background-color: #f0f0f0;
}

.sidebar a {
  text-decoration: none;
  color: #333;
  display: block;
}
</style>
