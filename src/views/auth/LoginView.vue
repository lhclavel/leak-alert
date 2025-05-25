<script setup>
import LoginForm from '@/components/auth/LoginForm.vue'
import { useDisplay } from 'vuetify'
</script>

<template>
  <!-- Simple styled header -->
  <div class="login-header">
    <div class="header-left"><span class="leak">Leak</span><span class="alert">Alert</span></div>
  </div>

  <!-- Login content -->
  <v-col cols="12" md="6" class="mx-auto">
    <v-card class="mx-auto" elevation="0">
      <v-card-text class="pt-4">
        <div class="d-flex justify-center">
          <img src="/images/logo1.png" style="max-width: 150px; height: 150px" alt="Logo" />
        </div>
        <h1 class="text-center mb-4">
          Hi! Welcome! <v-icon color="amber" size="32" class="ml-1">mdi-hand-wave</v-icon>
        </h1>

        <LoginForm></LoginForm>

        <v-divider class="my-5"></v-divider>

        <h4 class="text-center">
          Don't have account?
          <RouterLink class="text-primary" style="text-decoration: none" to="/register"
            >Register</RouterLink
          >
        </h4>
      </v-card-text>
    </v-card>
  </v-col>
</template>

<style scoped>
.login-header {
  background-color: #a1a1a1; /* same as your app header color */
  padding: 16px;
  display: flex;
  align-items: center;
  justify-content: flex-start; /* or center if you prefer */
  width: 100%;
  box-sizing: border-box;
}

/* Optional styling for your branding text inside the header */
.header-left {
  display: flex;
  align-items: center;
  font-size: 1.3rem;
  font-weight: bold;
  color: #fff;
}

.leak {
  color: black;
}
.alert {
  /* you can style this differently if needed */
  color: #2196f3;
}
</style>
