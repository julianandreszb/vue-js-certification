<script setup>
import ChildSlotScoped from '@/components/Component/Slot/ScopedSlots/ChildScopedSlot.vue'
</script>

<template>
  <ChildSlotScoped v-slot="slotProps">
    <p>Both values come from child:</p>
    <p>{{ `First Name: ${slotProps.firstName}` }}</p>
    <p>{{ `Last Name: ${slotProps.lastName}` }}</p>
  </ChildSlotScoped>
  <hr />

  <!-- OR with named slots-->
  <ChildSlotScoped>
    <template #default="{ firstName, lastName }">
      <p>Both values come from child:</p>
      <p>{{ `First Name: ${firstName}` }}</p>
      <p>{{ `Last Name: ${lastName}` }}</p>
    </template>
    <template #address="{ addressOne }">
      <p>Address: {{ addressOne }}</p>
    </template>
  </ChildSlotScoped>
</template>

<style scoped></style>
