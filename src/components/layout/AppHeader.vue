<script setup>
import { ref } from 'vue'
</script>

<template>
  <header class="app-header"><span class="leak">Leak</span><span class="alert">Alert</span></header>
</template>

<style scoped>
.app-header {
  background: #2196f3;
  padding: 8px 16px;
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
  letter-spacing: 0.5px;
  width: 100%;
  box-sizing: border-box;
}
.leak {
  color: #fff;
}
.alert {
  color: #222;
}
</style>
