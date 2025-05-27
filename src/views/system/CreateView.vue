<script setup>
import { ref, nextTick, onUnmounted } from 'vue'
import { useRouter } from 'vue-router'
import AppLayout from '@/components/layout/AppLayout.vue'

const selectedObject = ref('')
const description = ref('')
const selectedLocation = ref('Current Location')

const wideAngleImage = ref(null)
const videoRef = ref(null)
const stream = ref(null)
const showCamera = ref(false)
const showSuccessDialog = ref(false)
const isSubmitting = ref(false)

const objectOptions = ['Minor', 'Major', 'Emergency']

// Bottom navigation variables
const currentTab = ref('add')
const showCreateButton = ref(false)
const router = useRouter()

const handleSubmit = async () => {
  isSubmitting.value = true
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 1000))

    // Show success dialog
    showSuccessDialog.value = true

    // Reset form data
    selectedObject.value = ''
    description.value = ''
    selectedLocation.value = 'Current Location'
    wideAngleImage.value = null
  } catch (error) {
    console.error('Error submitting report:', error)
  } finally {
    isSubmitting.value = false
  }
}

// Add this new function
const handleCloseSuccess = () => {
  showSuccessDialog.value = false
  router.push('/dashboard')
}

// Bottom navigation functions
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

// Camera functions
const openCamera = async () => {
  try {
    stream.value = await navigator.mediaDevices.getUserMedia({
      video: {
        facingMode: 'environment',
      },
    })
    showCamera.value = true
    nextTick(() => {
      if (videoRef.value) {
        videoRef.value.srcObject = stream.value
      }
    })
  } catch (err) {
    console.error('Error accessing camera:', err)
  }
}

const capturePhoto = () => {
  const video = videoRef.value
  const canvas = document.createElement('canvas')
  canvas.width = video.videoWidth
  canvas.height = video.videoHeight
  canvas.getContext('2d').drawImage(video, 0, 0)
  wideAngleImage.value = canvas.toDataURL('image/jpeg')
  closeCamera()
}

const closeCamera = () => {
  if (stream.value) {
    stream.value.getTracks().forEach((track) => track.stop())
    stream.value = null
  }
  showCamera.value = false
}

onUnmounted(() => {
  closeCamera()
})
</script>

<template>
  <AppLayout>
    <template #content>
      <v-container class="pa-4">
        <!-- Camera Dialog -->
        <v-dialog v-model="showCamera" fullscreen class="camera-dialog">
          <div class="camera-container">
            <!-- Camera Preview -->
            <video ref="videoRef" autoplay playsinline class="camera-preview"></video>

            <!-- Camera UI Overlay -->
            <div class="camera-overlay">
              <!-- Top Bar -->
              <div class="top-bar">
                <v-btn icon class="top-btn" @click="closeCamera">
                  <v-icon color="white">mdi-close</v-icon>
                </v-btn>
              </div>

              <!-- Bottom Controls -->
              <div class="bottom-section">
                <!-- Mode Selection -->
                <div class="mode-selector">
                  <div class="mode-text">Portrait</div>
                  <div class="mode-text active">Camera</div>
                  <div class="mode-text">Video</div>
                </div>

                <!-- Camera Controls -->
                <div class="camera-controls">
                  <div class="control-btn gallery-btn">
                    <v-icon color="white" size="24">mdi-image</v-icon>
                  </div>

                  <div class="shutter-btn" @click="capturePhoto">
                    <div class="shutter-btn-inner"></div>
                  </div>

                  <div class="control-btn flip-btn">
                    <v-icon color="white" size="24">mdi-camera-flip</v-icon>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </v-dialog>

        <!-- Take a picture section -->
        <div class="mb-4">
          <div class="d-flex align-center my-2">
            <v-divider class="flex-grow-1"></v-divider>
            <span class="mx-1 text-caption">Take</span>
            <span class="mx-1 text-caption">Picture</span>
            <v-divider class="flex-grow-1"></v-divider>
          </div>
          <v-row>
            <v-col cols="6">
              <v-card
                class="d-flex flex-column align-center justify-center pa-6"
                height="120"
                variant="outlined"
                style="border-style: dashed; cursor: pointer; position: relative; overflow: hidden"
                @click="openCamera"
              >
                <!-- Show captured image if exists -->
                <v-img
                  v-if="wideAngleImage"
                  :src="wideAngleImage"
                  cover
                  height="100%"
                  width="100%"
                  style="position: absolute"
                >
                  <div class="image-overlay d-flex align-center justify-center">
                    <v-icon size="32" color="white">mdi-camera</v-icon>
                  </div>
                </v-img>

                <!-- Show placeholder if no image -->
                <template v-else>
                  <v-icon size="32" color="grey-darken-1" class="mb-2">mdi-camera</v-icon>
                  <span class="text-caption text-grey-darken-1">Wide Angle</span>
                </template>
              </v-card>
            </v-col>
            <v-col cols="6">
              <v-card
                class="d-flex flex-column align-center justify-center pa-6"
                height="120"
                variant="outlined"
                style="border-style: dashed"
              >
                <v-icon size="32" color="grey-darken-1" class="mb-2"> mdi-camera </v-icon>
                <span class="text-caption text-grey-darken-1">Close-up</span>
              </v-card>
            </v-col>
          </v-row>
        </div>

        <!-- Change Location section -->
        <div class="mb-8">
          <h2 class="text-h6 font-weight-medium mb-3">Change Location</h2>
          <v-card class="pa-3" color="grey-lighten-4">
            <!-- Map placeholder -->
            <div
              class="mb-3"
              style="
                height: 120px;
                border-radius: 8px;
                background: linear-gradient(135deg, #c8e6c9 0%, #a5d6a7 100%);
                position: relative;
                overflow: hidden;
              "
            >
              <!-- Simple map lines -->
              <div
                style="
                  position: absolute;
                  top: 8px;
                  left: 8px;
                  right: 8px;
                  height: 2px;
                  background: #ffc107;
                  border-radius: 1px;
                "
              ></div>
              <div
                style="
                  position: absolute;
                  top: 20px;
                  left: 16px;
                  right: 32px;
                  height: 2px;
                  background: #ffb300;
                  border-radius: 1px;
                "
              ></div>
              <div
                style="
                  position: absolute;
                  bottom: 16px;
                  left: 12px;
                  width: 6px;
                  height: 6px;
                  background: #f44336;
                  border-radius: 50%;
                "
              ></div>
              <div
                style="
                  position: absolute;
                  bottom: 24px;
                  right: 16px;
                  width: 2px;
                  height: 12px;
                  background: #2196f3;
                  border-radius: 1px;
                "
              ></div>
            </div>

            <div class="d-flex align-center justify-space-between">
              <div class="d-flex align-center">
                <v-icon size="16" color="grey-darken-1" class="mr-2"> mdi-map-marker </v-icon>
                <span class="text-body-2 text-grey-darken-2">{{ selectedLocation }}</span>
              </div>
              <v-icon size="16" color="grey-darken-1"> mdi-chevron-down </v-icon>
            </div>
          </v-card>
        </div>

        <!-- General Information section -->
        <div class="mb-8">
          <h2 class="text-h6 font-weight-medium mb-3">General Information</h2>
          <div class="mb-4">
            <v-select
              v-model="selectedObject"
              :items="objectOptions"
              label="Select Options"
              variant="outlined"
              density="comfortable"
              placeholder="Select an option"
            ></v-select>
          </div>

          <v-textarea
            v-model="description"
            label="Description"
            variant="outlined"
            density="comfortable"
            placeholder="Enter description..."
            rows="3"
            no-resize
          ></v-textarea>
        </div>

        <!-- Submit button -->

        <v-dialog v-model="showSuccessDialog" persistent max-width="300" class="success-overlay">
          <v-card class="success-dialog">
            <v-card-text class="text-center pa-6">
              <v-icon color="primary" size="64" class="mb-4">mdi-check-circle</v-icon>
              <h3 class="text-h6 mb-2">Success!</h3>
              <p class="text-body-1 text-medium-emphasis mb-4">Your report has been submitted</p>
              <v-btn color="primary" block @click="handleCloseSuccess" class="text-none">
                Done
              </v-btn>
            </v-card-text>
          </v-card>
        </v-dialog>

        <!-- Update the existing submit button to show loading state -->
        <v-btn
          @click="handleSubmit"
          color="primary"
          size="large"
          block
          class="text-none font-weight-medium"
          :loading="isSubmitting"
        >
          Submit Report
        </v-btn>
      </v-container>
    </template>
  </AppLayout>
</template>

<style scoped>
.v-container {
  max-width: 400px;
  margin: 0 auto;
  padding-bottom: 70px; /* Add padding to prevent content overlap with bottom nav */
}

/* Bottom Navigation */
.bottom-nav {
  position: fixed; /* Fix the bottom nav to the bottom of the screen */
  bottom: 0;
  left: 0;
  width: 100%;
  display: flex;
  background: #2196f3;
  height: 70px;
  border-top: 1px solid #e0e0e0;
  z-index: 1000; /* Ensure it stays above other content */
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

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.v-card:hover .image-overlay {
  opacity: 1;
}

.v-dialog {
  background: black;
}

video {
  background: black;
}

.camera-dialog {
  background: black;
}

.camera-container {
  position: relative;
  height: 100vh;
  background: black;
}

.camera-preview {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.camera-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.top-bar {
  padding: 16px;
  display: flex;
  justify-content: flex-start;
}

.top-btn {
  background: rgba(0, 0, 0, 0.4) !important;
  border-radius: 50%;
}

.bottom-section {
  padding-bottom: 48px;
}

.mode-selector {
  display: flex;
  justify-content: center;
  gap: 32px;
  margin-bottom: 24px;
}

.mode-text {
  color: rgba(255, 255, 255, 0.7);
  font-size: 14px;
  font-weight: 500;
  text-transform: none;
}

.mode-text.active {
  color: white;
}

.camera-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 48px;
}

.control-btn {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
}

.shutter-btn {
  width: 76px;
  height: 76px;
  border-radius: 50%;
  border: 4px solid white;
  padding: 2px;
  background: transparent;
  cursor: pointer;
}

.shutter-btn-inner {
  width: 100%;
  height: 100%;
  background: white;
  border-radius: 50%;
}

.gallery-btn,
.flip-btn {
  opacity: 0.9;
}

.success-overlay {
  background-color: rgba(255, 255, 255, 0.178) !important;
}

.success-dialog {
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.1);
}

.v-card-text {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
