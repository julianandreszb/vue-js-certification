<script setup>
import { ref } from 'vue'

const firstName = ref('Julian')

defineExpose({
  firstName
})
</script>

<template>{{ firstName }}</template>

<style scoped></style>
