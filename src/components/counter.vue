<script setup>
import { ref } from "vue";

const counter = ref(0);

function increment() {
  counter.value++;
}

function decrement() {
  counter.value--;
}

function reset() {
  counter.value = 0;
}
</script>

<template>
  <div>
    <h1>Counter:{{ counter }}</h1>
    <button @click="increment">INCREMENT</button>
    <button @click="decrement">DECREMENT</button>
    <button @click="reset">RESET</button>
  </div>
</template>

<style lang="scss" scoped>


button {
  margin: 5px;
  padding: 10px;
  font-size: 16px;
}
</style>
