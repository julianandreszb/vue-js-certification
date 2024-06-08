<script setup>
import SlotChild from '@/components/Component/Slot/SlotChild.vue'
</script>

<template>
  <SlotChild>
    <div :style="{ backgroundColor: 'red' }">
      <h1>SlotChild</h1>
    </div>
  </SlotChild>
</template>

<style scoped></style>
