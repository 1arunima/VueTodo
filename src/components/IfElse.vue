<template>
  <div>
    <!-- Conditional rendering based on the isLoggedIn variable -->
    <h1 v-if="isLoggedIn">Welcome back, User!</h1>
    <h1 v-else>Please log in.</h1>

    <!-- Button to toggle login state for demonstration -->
    <button @click="toggleLogin">Toggle Login State</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Simulate the login state with a boolean variable
const isLoggedIn = ref(false)

// Method to toggle the login state
function toggleLogin() {
  isLoggedIn.value = !isLoggedIn.value
}
</script>

<style scoped>
button {
  margin-top: 20px;
  padding: 10px;
  background-color: #4caf50;
  color: white;
  font-size: 16px;
}
h1 {
  font-size: 24px;
  margin: 20px 0;
}
</style>
