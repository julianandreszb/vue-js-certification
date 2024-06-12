<script setup>
const counter = defineModel()

function increment() {
  counter.value++
}
</script>

<template>
  <button @click="increment">Increase Counter</button>
  <p>Counter on child {{ counter }}</p>
</template>

<style scoped></style>
