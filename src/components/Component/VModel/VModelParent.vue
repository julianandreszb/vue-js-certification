<script setup>
import VModelChild from '@/components/Component/VModel/VModelChild.vue'
import { ref } from 'vue'
const counter = ref(0)
</script>

<template>
  <h1>v-model</h1>
  <p>Counter on parent: {{ counter }}</p>
  <VModelChild v-model="counter" />
</template>

<style scoped></style>
