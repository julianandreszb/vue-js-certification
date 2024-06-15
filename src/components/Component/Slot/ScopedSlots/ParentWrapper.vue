<script setup>
import ChildSlotScoped from '@/components/Component/Slot/ScopedSlots/ChildSlotScoped.vue'
</script>

<template>
  <ChildSlotScoped v-slot="slotProps">
    {{
      `First Name: ${slotProps.firstName}, Last Name: ${slotProps.lastName} (Both values come from child)`
    }}
  </ChildSlotScoped>
</template>

<style scoped></style>
