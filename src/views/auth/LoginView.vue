<script setup>
import AppHeader from '@/components/layout/AppHeader.vue'
import LoginForm from '@/components/auth/LoginForm.vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>

<template>
  <div>
    <AppHeader />

    <v-col cols="12" md="6" class="mx-auto pt-16">
      <v-card class="mx-auto" elevation="0">
        <v-card-text class="pt-4">
          <h1 class="text-center mb-16">Hi! Welcome Back!</h1>
          <v-divider class="my-5"></v-divider>

          <LoginForm></LoginForm>

          <v-divider class="my-5"></v-divider>

          <h5 class="text-center">
            Don't have account?
            <RouterLink class="text-primary" to="/register">Click Here to Register</RouterLink>
          </h5>
        </v-card-text>
      </v-card>
    </v-col>
  </div>
</template>
