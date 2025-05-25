<script setup>
import AppHeader from '@/components/layout/AppHeader.vue'
import RegisterForm from '@/components/auth/RegisterForm.vue'
</script>

<template>
  <div>
    <AppHeader />
    <v-col cols="11" md="6" class="mx-auto">
      <v-card class="py-6" elevation="0">
        <div class="text-center">
          <h2 class="mb-6 font-weight-bold">Create an Account</h2>
        </div>

        <RegisterForm />

        <h4 class="text-center">
          Already have an account?
          <RouterLink to="/login" class="text-primary" style="text-decoration: none"
            >Login</RouterLink
          >
        </h4>
      </v-card>
    </v-col>
  </div>
</template>
