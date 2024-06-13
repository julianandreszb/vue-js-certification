<script setup>
import VModelChild from '@/components/Component/VModel/VModelChild.vue'
import { ref } from 'vue'
const counter = ref(0)
const firstName = ref('Julian')
</script>

<template>
  <h1>v-model</h1>
  <p>Counter on parent: {{ counter }}</p>
  <p>First Name on parent: {{ firstName }}</p>
  <hr />

  <VModelChild v-model="counter" v-model:first-name="firstName" />
</template>

<style scoped></style>
