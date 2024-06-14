<script setup>
import SlotChild from '@/components/Component/Slot/SlotChild.vue'
import SlotChildDefaultValue from '@/components/Component/Slot/SlotChildDefaultValue.vue'
import SlotChildNamedSlots from '@/components/Component/Slot/SlotChildNamedSlots.vue'
</script>

<template>
  <p>Slot content:</p>
  <SlotChild>
    <div :style="{ backgroundColor: 'red' }">
      <h1>SlotChild</h1>
    </div>
  </SlotChild>

  <hr>
  <p>Slot with default value:</p>
  <SlotChildDefaultValue />
  
  <hr>
  
  <p>Named slots:</p>
  <SlotChildNamedSlots>
    <template v-slot:title><h1>This is the title slot</h1></template>
    <template v-slot:body><p>This is the content slot</p></template>
  </SlotChildNamedSlots>
</template>

<style scoped></style>
