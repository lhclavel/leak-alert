<script setup>
import { ref } from 'vue'

const isSidebarOpen = ref(false)
const fileInput = ref(null)

// Toggle sidebar menu
function toggleSidebar() {
  isSidebarOpen.value = !isSidebarOpen.value
}

// Handle logout
function logout() {
  window.location.href = '/login'
}

const user = {
  name: 'John Doe',
  email: 'johndoe@gmail.com',
  avatar: '/path/to/your/avatar.jpg',
}

// Add FAQ data
const faqs = ref([
  {
    question: 'What is Leak Alert?',
    answer: 'Leak Alert is a system that notifies users about water or gas leaks in real-time.',
  },
  {
    question: 'How do I report a leak?',
    answer: 'Go to the dashboard and click on "Report a Leak" to submit details.',
  },
  {
    question: 'Can I reset my password?',
    answer: 'Yes, click on "Forgot Password?" on the login page to reset it.',
  },
])

function triggerFileUpload() {
  fileInput.value.click()
}

function onFileChange(event) {
  const file = event.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = (e) => {
      user.avatar = e.target.result
    }
    reader.readAsDataURL(file)
  }
}
</script>

<template>
  <header class="app-header">
    <div class="header-left"><span class="leak">Leak</span><span class="alert">Alert</span></div>
    <div class="menu-container">
      <button class="menu-btn" @click="toggleSidebar" aria-label="Menu">☰</button>
      <!-- Sidebar menu -->
      <div :class="['sidebar', { 'sidebar-open': isSidebarOpen }]">
        <button class="close-btn" @click="toggleSidebar">
          <v-icon>mdi-chevron-left</v-icon>
        </button>
        <ul>
          <!-- Profile Section -->
          <div class="profile-section">
            <div class="profile-info">
              <div class="avatar-container" @click="triggerFileUpload">
                <v-avatar size="80">
                  <v-img :src="user.avatar" alt="Profile"></v-img>
                  <div class="change-photo-overlay">
                    <v-icon color="white" size="24">mdi-camera</v-icon>
                  </div>
                </v-avatar>
                <input
                  ref="fileInput"
                  type="file"
                  accept="image/*"
                  @change="onFileChange"
                  style="display: none"
                />
              </div>
              <h3 class="username">{{ user.name }}</h3>
              <p class="email">{{ user.email }}</p>
              <v-btn variant="flat" class="edit-btn">Edit Profile</v-btn>
            </div>
          </div>
          <v-divider class="my-5"></v-divider>
          <li>
            <a href="#" @click.prevent="logout"> <span class="mdi mdi-logout me-2"></span>Logout</a>
          </li>
          <v-divider class="my-5"></v-divider>
          <div class="faq-section">
            <h3 class="text-subtitle-1 text-white font-weight-medium px-4 mb-3 text-center">FAQ</h3>
            <div v-for="faq in faqs" :key="faq.question" class="faq-item">
              <p class="faq-question">{{ faq.question }}</p>
              <p class="faq-answer">{{ faq.answer }}</p>
            </div>
          </div>
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

.profile-section {
  text-align: center;
  padding: 20px;
  position: relative;
}

.profile-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
}

.verify-icon {
  position: absolute;
  right: calc(50% - 45px);
  bottom: 85px;
  background: #263b7e;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid white;
}

.profile-section h3 {
  margin: 10px 0 0;
  font-size: 16px;
  color: #333;
}

.profile-section p {
  margin: 5px 0;
  font-size: 14px;
  color: #666;
}

.change-photo-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 1;
  transition: opacity 0.3s ease;
  z-index: 1102; /* Higher than sidebar and menu button */
}

.avatar-container {
  position: relative;
  cursor: pointer;
  z-index: 1102; /* Higher than sidebar and menu button */
}

.avatar-container:hover .change-photo-overlay {
  opacity: 1;
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
  z-index: 1100; /* Lower than the menu button */
  transition: right 0.3s ease; /* Add smooth transition */
  padding-top: 70px; /* Increased to accommodate close button */
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
  right: 0;
}

.close-btn {
  position: absolute;
  top: 10px;
  left: 8px;
  background: transparent;
  border: none;
  color: #333;
  cursor: pointer;
  padding: 2px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease;
}

.close-btn:hover {
  transform: translateX(-4px);
}

.faq-section {
  padding: 0 12px;
  margin-top: 8px;
  margin-bottom: 16px;
}

.faq-item {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  padding: 12px;
  margin-bottom: 8px;
  transition: background-color 0.2s ease;
}

.faq-item:hover {
  background: rgba(255, 255, 255, 0.15);
}
.faq-question {
  color: white;
  font-size: 14px;
  font-weight: 500;
  margin-bottom: 8px;
  text-align: justify;
}

.faq-answer {
  color: rgba(255, 255, 255, 0.8);
  font-size: 12px;
  line-height: 1.4;
  text-align: justify;
}
</style>
