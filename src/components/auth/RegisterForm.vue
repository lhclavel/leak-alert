<script setup>
import { ref } from 'vue'

const show = ref(false)
const password = ref('')
const confirmPassword = ref('')
const firstname = ref('')
const lastname = ref('')
const email = ref('')
</script>

<template>
  <v-form fast-fail @submit.prevent>
    <div class="mb-2">
      <label class="custom-label" for="register-firstname"></label>
      <v-text-field
        id="register-firstname"
        v-model="firstname"
        placeholder="Enter your username"
        variant="outlined"
        class="my-1 rounded-input"
        prepend-inner-icon="mdi-account"
        required
      />
    </div>

    <div class="mb-2">
      <label class="custom-label" for="register-lastname"></label>
      <v-text-field
        id="register-lastname"
        v-model="lastname"
        placeholder="Enter your email"
        variant="outlined"
        class="my-1 rounded-input"
        prepend-inner-icon="mdi-email"
        required
      />
    </div>

    <div class="mb-2">
      <label class="custom-label" for="register-email"></label>
      <v-text-field
        id="register-email"
        v-model="email"
        placeholder="Phone Number"
        variant="outlined"
        class="my-1 rounded-input"
        prepend-inner-icon="mdi-phone"
        type="email"
        required
      />
    </div>

    <div class="mb-2">
      <label class="custom-label" for="register-password"> </label>
      <v-text-field
        id="register-password"
        v-model="password"
        placeholder="Enter your password"
        variant="outlined"
        class="my-1 rounded-input"
        prepend-inner-icon="mdi-lock"
        :append-inner-icon="show ? 'mdi-eye-off' : 'mdi-eye'"
        :type="show ? 'text' : 'password'"
        @click:append-inner="show = !show"
        required
      />
    </div>

    <v-btn
      class="my-3 same-height-btn"
      type="submit"
      block
      color="primary"
      style="border-radius: 10px"
    >
      Sign Up
    </v-btn>

    <div class="d-flex align-center my-8">
      <v-divider class="flex-grow-1"></v-divider>
      <span class="mx-1 text-caption">Or</span>
      <span class="mx-1 text-caption">With</span>
      <v-divider class="flex-grow-1"></v-divider>
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
      class="mb-8 text-black same-height-btn google-btn"
      style="border-radius: 10px"
    >
      <img
        src="/images/google-logo.png"
        alt="Google"
        style="width: 18px; height: 18px; margin-right: 8px"
      />
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

.rounded-input :deep(.v-field__outline) {
  border-radius: 10px !important;
}

.rounded-input :deep(.v-field) {
  border-radius: 10px !important;
}

.rounded-input :deep(.v-field__input) {
  padding-left: 12px !important;
}

.rounded-input :deep(.v-input__prepend) {
  margin-right: 4px !important;
}
</style>
