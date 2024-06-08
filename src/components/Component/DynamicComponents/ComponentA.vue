<script setup>
import { onActivated, onDeactivated } from 'vue'

onActivated(() => {
  console.log('Component A is activated')
})

onDeactivated(() => {
  console.log('Component A is deactivated')
})
</script>

<template>
  <div>
    <h1>Component A</h1>
    <p>This is the component A</p>
  </div>
</template>

<style scoped></style>
