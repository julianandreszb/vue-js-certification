<script setup>
import { ref } from 'vue'
import ComponentA from '@/components/Component/DynamicComponents/ComponentA.vue'
import ComponentB from '@/components/Component/DynamicComponents/ComponentB.vue'

const components = {
  ComponentA,
  ComponentB
}

const currentComponent = ref('ComponentA')
</script>

<template>
  <button v-for="(_, comp) in components" :key="comp" @click="currentComponent = comp">
    Show {{ comp }}
  </button>
  <component :is="components[currentComponent]" />

  <!-- KeepAlive: Inactive components will be cached (Keep state)! -->
  <KeepAlive>
    <component :is="components[currentComponent]" />
  </KeepAlive>
</template>

<style scoped></style>
