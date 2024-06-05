<script setup>
import { reactive, ref, watch } from 'vue'

// Watch single ref
const firstName = ref('Julian')
watch(firstName, (newVal, oldVal) => {
  console.log(`New first name: ${newVal}, old first name: ${oldVal}`)
})

// Watch getter
const x = ref(1)
const y = ref(2)
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

// Watch a reactive object
const person = reactive({
  firstName: 'Julian',
  lastName: 'Schmidt'
})

// This will NOT work. Both (newPerson, oldPerson) will be the same object because they both point to the same object!
// watch(person, (newPerson, oldPerson) => {
//   console.log(`New person: ${JSON.stringify(newPerson)}\nOld person: ${JSON.stringify(oldPerson)}`)
// })

// This will work, reactive internally convert the object properties into refs.
watch(
  () => person.firstName, // person.firstName = ref
  (newPersonFirstName, oldPersonFirstName) => {
    console.log(
      `New person.firstName: ${JSON.stringify(newPersonFirstName)}\nOld person.firstName: ${JSON.stringify(oldPersonFirstName)}`
    )
  }
)
</script>

<template>
  <label for="firstName">First name: </label>
  <input id="firstName" type="text" v-model="firstName" />

  <br />
  <br />

  <label for="x">X: </label>
  <input id="x" type="number" v-model="x" />

  <br />

  <label for="y">Y: </label>
  <input id="y" type="number" v-model="y" />

  <br />
  <br />

  <label for="person">Person First Name: </label>
  <input id="person" type="text" v-model="person.firstName" />
</template>

<style scoped></style>
