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
    Show {{ comp }} - {{ _ }}
  </button>
  <component :is="components[currentComponent]" />

  <hr />

  <!-- KeepAlive: Inactive components will be cached (Keep state)! -->
  <!-- onActivated and onDeactivated are only called when KeepAlive wraps the component tag -->
  <span>Using KeepAlive (It keeps the state):</span>
  <KeepAlive>
    <component :is="components[currentComponent]" />
  </KeepAlive>
</template>

<style scoped></style>
