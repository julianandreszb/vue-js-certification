<script setup>
import { onMounted, ref } from 'vue'

const inputRef = ref(null)

onMounted(() => {
  console.log(`onMounted.inputRef`, inputRef) // It must print <input>
  inputRef.value.focus()
})
</script>

<template>
  <input ref="inputRef" type="text" name="name" />
</template>

<style scoped>
input:focus {
  background-color: red;
}
</style>
