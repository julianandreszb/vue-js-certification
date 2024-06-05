<script setup>
import { onBeforeMount, onBeforeUnmount, onMounted, onUnmounted, onUpdated, ref } from 'vue'

onBeforeMount(() => {console.log('onBeforeMount')})

onMounted(() => {console.log('onMounted')})

onUpdated(()=> {console.log('onUpdated')})

onUnmounted(() => {console.log('onUnmounted')})

onBeforeUnmount(()=>{console.log('onBeforeUnmount')})

const name = ref('hello')
</script>

<template>
  {{ name  }}
  <br>
  <button @click="name = 'world'">Change to world</button>
</template>

<style scoped>

</style>