<script setup>
import { onActivated, onDeactivated, ref } from 'vue'

onActivated(() => {
  console.log('Component A is activated')
})

onDeactivated(() => {
  console.log('Component A is deactivated')
})

const counter = ref(0)
function increment() {
  counter.value++
}
</script>

<template>
  <div>
    <h1>Component A</h1>
    <p>This is the component A</p>
    {{ counter }}
    <button @click="increment">Increment</button>
  </div>
</template>

<style scoped></style>
