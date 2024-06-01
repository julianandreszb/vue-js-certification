<script setup>
import { ref, watch } from 'vue'

const firstName = ref('Julian')

const x = ref(1)
const y = ref(2)

// Watch single ref
watch(firstName, (newVal, oldVal) => {
  console.log(`New first name: ${newVal}, old first name: ${oldVal}`)
})

// Watch getter
watch(
  () => x.value + y.value,
  (newSum, oldSum) => {
    console.log(`New sum: ${newSum}, old sum: ${oldSum}`)
  }
)

// Watch multiple refs using array
watch([x, () => y.value], ([newValueX, newValueY], [oldValueX, oldValueY]) => {
  console.log(`(Using array) New value of X: ${newValueX}, old value of X: ${oldValueX}`)
  console.log(`(Using array) New value of Y: ${newValueY}, old value of X: ${oldValueY}`)
})
</script>

<template>
  <input type="text" v-model="firstName" />

  <br />

  <label for="x"></label>
  <input id="x" type="number" v-model="x" />

  <br />

  <label for="y"></label>
  <input id="y" type="number" v-model="y" />
</template>

<style scoped></style>
