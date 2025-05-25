<script setup>
import RegisterForm from '@/components/auth/RegisterForm.vue'
</script>

<template>
  <!-- Simple styled header -->
  <div class="login-header">
    <div class="header-left"><span class="leak">Leak</span><span class="alert">Alert</span></div>
  </div>

  <div>
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
