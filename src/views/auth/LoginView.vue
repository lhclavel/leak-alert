<script setup>
import AppHeader from '@/components/layout/AppHeader.vue'
import LoginForm from '@/components/auth/LoginForm.vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>

<template>
  <div>
    <AppHeader />

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
  </div>
</template>
