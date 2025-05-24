<template>
  <v-container class="fill-height d-flex flex-column align-center justify-center">
    <img src="/images/logo1.png" style="max-width: 200px; margin-bottom: 24px" />
    <div class="text-h4 font-weight-bold">Leak<span class="text-primary">Alert</span></div>
  </v-container>
</template>

<script setup>
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

onMounted(() => {
  setTimeout(() => {
    router.replace('/login')
  }, 2000)
})
</script>

<style scoped>
.fill-height {
  min-height: 100vh;
  background: #fff;
}
</style>
