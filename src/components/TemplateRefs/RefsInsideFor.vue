<script setup>
import { onMounted, ref } from 'vue'

const liRefs = ref([])
onMounted(() => {
  liRefs.value.forEach((el) => {
    console.log(el.textContent)
  })
})
</script>

<template>
  <ul>
    <li v-for="i in 3" ref="liRefs" :key="i">List item {{ i + 1 }}</li>
  </ul>
</template>

<style scoped></style>
