<script setup>
import { ref } from 'vue'
const show = ref(false)
const password = ref('')
</script>
<template>
  <v-form fast-fail @submit.prevent>
    <div class="mb-1">
      <label class="custom-label" for="login-email">Email</label>
      <v-text-field
        id="login-email"
        label=""
        placeholder="example@gmail.com"
        variant="outlined"
        class="my-1"
        prepend-inner-icon="mdi-email"
        type="email"
        required
      ></v-text-field>
    </div>

    <div class="mb-1">
      <label class="custom-label" for="login-password">Password</label>
      <v-text-field
        id="login-password"
        label=""
        variant="outlined"
        class="my-1"
        prepend-inner-icon="mdi-lock"
        :append-inner-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
        :type="show ? 'text' : 'password'"
        @click:append-inner="show = !show"
        required
        v-model="password"
      ></v-text-field>
    </div>

    <div class="d-flex justify-space-between align-center mb-2">
      <v-checkbox
        label="Remember Me"
        hide-details
        density="compact"
        class="ma-0 pa-0"
        style="margin-left: -10px"
      ></v-checkbox>
      <RouterLink class="text-primary text-caption" to="/forgot-password"
        >Forgot Password?</RouterLink
      >
    </div>

    <v-btn class="mt-2 mb-2 same-height-btn" type="submit" block color="primary">Sign In</v-btn>

    <div class="d-flex align-center my-6">
      <v-divider class="flex-grow-1"></v-divider>
      <span class="mx-1 text-caption">or</span>
      <span class="mx-1 text-caption">with</span> <v-divider class="flex-grow-1"></v-divider>
    </div>

    <v-btn
      block
      color="primary"
      class="mb-6 same-height-btn"
      prepend-icon="mdi-facebook"
      style="border-radius: 10px"
    >
      Sign Up with Facebook
    </v-btn>
    <v-btn
      block
      color="white"
      class="mb-6 text-black same-height-btn google-btn"
      prepend-icon="mdi-google"
      style="border-radius: 10px"
    >
      Sign Up with Google
    </v-btn>
  </v-form>
</template>

<style scoped>
.v-btn {
  text-transform: none !important;
}
.same-height-btn {
  height: 40px !important;
  min-height: 50px !important;
  font-size: 1rem;
}

.google-btn {
  border: 1px solid #000 !important;
}

/* Fix for black border and rounded corners on Vuetify 3 outlined text fields */
.v-text-field--outlined .v-field__outline {
  border-radius: 30px !important;
  border-color: #000 !important;
  border-width: 1.5px !important;
  /* fallback for browsers that support border shorthand */
  border-style: solid !important;
}
</style>
