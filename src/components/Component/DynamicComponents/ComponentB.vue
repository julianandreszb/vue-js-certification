<script setup>
import { ref } from 'vue'

const counter = ref(0)
function increment() {
  counter.value++
}
</script>

<template>
  <div>
    <h1>Component B</h1>
    <p>This is the component B</p>

    {{ counter }}
    <button @click="increment">Increment</button>
  </div>
</template>

<style scoped></style>
