<script setup>
import { ref } from 'vue'

const form = ref(null)
const email = ref('')
const password = ref('')
const emailRules = [
  v => !!v || 'Email is required',
  v => (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(v)) || 'Email must be a valid e-mail.',
]
const checkbox = ref(false)

const validate = async () => {
  const { valid } = await form.value.validate()

  if (valid) alert('Form is valid')
}
const reset = () => {
  form.value.reset()
}
const resetValidation = () => {
  form.value.resetValidation()
}
</script>

<template>
  <h1>Login</h1>
  <v-sheet width="300">
    <v-form ref="form">
      <v-text-field
        v-model="email"
        :counter="10"
        :rules="emailRules"
        label="Email"
        type="email"
        required
      ></v-text-field>

      <v-text-field
        v-model="password"
        :counter="10"
        :rules="[v => !!v || 'Password is required']"
        label="Password"
        type="password"
        required
      ></v-text-field>

      <v-checkbox
        v-model="checkbox"
        :rules="[v => !!v || 'You must agree to continue!']"
        label="Do you agree?"
        required
      ></v-checkbox>

      <div class="d-flex flex-column">
        <v-btn
          color="success"
          class="mt-4"
          block
          @click="validate"
        >
          Validate
        </v-btn>

        <v-btn
          color="error"
          class="mt-4"
          block
          @click="reset"
        >
          Reset Form
        </v-btn>

        <v-btn
          color="warning"
          class="mt-4"
          block
          @click="resetValidation"
        >
          Reset Validation
        </v-btn>
      </div>
    </v-form>
  </v-sheet>
</template>
