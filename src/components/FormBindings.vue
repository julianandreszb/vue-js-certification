<script setup>
import { ref } from 'vue'

const firstName = ref('')
const lastName = ref('')

const countrySelected = ref('co')
const countryOptions = ref([
  { text: 'Colombia', value: 'co' },
  { text: 'Argentina', value: 'ar' }
])
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

    <div>
      <label for="country"></label>
      <select name="country" id="country">
        <option value="" disabled>Select one option</option>
        <option v-for="country in countryOptions" :value="country.value" :key="country.value">
          {{ country.text }}
        </option>
      </select>
      <p>Country selected: {{ countrySelected }}</p>
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
