<script setup>
import { ref } from 'vue'
const show = ref(false)
const password = ref('')
</script>

<template>
  <v-form fast-fail @submit.prevent>
    <v-text-field
      label="Email"
      variant="outlined"
      class="mb-2"
      prepend-inner-icon="mdi-email"
      type="email"
      required
    ></v-text-field>

    <v-text-field
      label="Password"
      variant="outlined"
      class="mb-2"
      prepend-inner-icon="mdi-lock"
      :append-inner-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
      :type="show ? 'text' : 'password'"
      @click:append-inner="show = !show"
      required
      v-model="password"
    ></v-text-field>

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

    <v-btn class="mt-2 mb-2" type="submit" block color="primary">Sign In</v-btn>

    <div class="d-flex align-center my-2">
      <v-divider class="flex-grow-1"></v-divider>
      <span class="mx-2 text-caption">Or With</span>
      <v-divider class="flex-grow-1"></v-divider>
    </div>

    <v-btn block color="blue darken-4" class="mb-2" prepend-icon="mdi-facebook">
      Sign Up with Facebook
    </v-btn>
    <v-btn block color="white" class="mb-2 text-black" prepend-icon="mdi-google">
      Sign Up with Google
    </v-btn>
  </v-form>
</template>

<style scoped>
.v-text-field--outlined .v-field__outline__start,
.v-text-field--outlined .v-field__outline__end,
.v-text-field--outlined .v-field__outline__notch {
  border-color: #000 !important;
  border-width: 2px !important;
  border-radius: 8px !important;
}
</style>
