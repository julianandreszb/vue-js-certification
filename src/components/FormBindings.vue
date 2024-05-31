<script setup>
import { ref } from 'vue'

const firstName = ref('')
const lastName = ref('')
</script>

<template>
  <form action="">
    <div>
      <label for="firstName">First Name (Using v-model)</label>
      <input v-model="firstName" type="text" name="firstName" id="firstName" />
      <p>{{ firstName }}</p>
    </div>

    <div>
      <label for="lastName">Last Name (Using v-bind + v-on:input)</label>
      <input
        v-bind:value="lastName"
        type="text"
        v-on:input="lastName = $event.target.value /* (event) => (lastName = event.target.value)*/"
        name="lastName"
        id="lastName"
      />
      <p>{{ lastName }}</p>
    </div>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

label {
  margin-top: 1rem;
}
</style>
