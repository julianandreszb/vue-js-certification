<script setup>
import VModelChild from '@/components/Component/VModel/VModelChild.vue'
import { ref } from 'vue'
const counter = ref(0)
const userName = ref('Julian')
</script>

<template>
  <h1>v-model</h1>
  <p>Counter on parent: {{ counter }}</p>
  <p>User Name: {{ userName }}</p>
  <VModelChild v-model="counter" v-model:first-name="userName" />
</template>

<style scoped></style>
