<script setup>
const counter = defineModel()

const firstName = defineModel('firstName')

function increment() {
  counter.value++
}
</script>

<template>
  <button @click="increment">Increase Counter</button>
  <p>Counter on child {{ counter }}</p>

  <p>First Name on child {{ firstName }}</p>
  <input type="text" v-model="firstName" />
</template>

<style scoped></style>
