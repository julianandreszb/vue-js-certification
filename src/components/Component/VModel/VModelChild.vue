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

  <hr>
  <label for="firstNameInput">First Name</label>
  <input id="firstNameInput" type="text" v-model="firstName" >
</template>

<style scoped></style>
