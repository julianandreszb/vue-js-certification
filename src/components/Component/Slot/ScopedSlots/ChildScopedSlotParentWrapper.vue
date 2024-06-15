<script setup>
import ChildSlotScoped from '@/components/Component/Slot/ScopedSlots/ChildScopedSlot.vue'
</script>

<template>
  <ChildSlotScoped v-slot="slotProps">
    <p>Both values come from child:</p>
    <p>{{ `First Name: ${slotProps.firstName}` }}</p>
    <p>{{ `Last Name: ${slotProps.lastName}` }}</p>
  </ChildSlotScoped>
</template>

<style scoped></style>
