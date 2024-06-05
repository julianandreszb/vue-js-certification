<script setup>
import { ref } from 'vue'
import LifecycleChild from '@/components/LifecycleChild.vue'
const isMounted = ref(true)

</script>

<template>
  <LifecycleChild  v-if="isMounted" />
  <br>
  <button @click="() => isMounted = false" >Unmount Lifecycle</button>
</template>

<style scoped>

</style>