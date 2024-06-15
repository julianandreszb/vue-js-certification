<script setup>
import SlotFancyListChild from '@/components/Component/Slot/FancyList/SlotFancyListChild.vue'
const loadingTimeout = 1000
</script>

<template>
  <SlotFancyListChild :loadingTimeout="loadingTimeout">
    <template #item="itemProps">
      <p>
        {{
          `ID: ${itemProps.itemData.id} - First Name: ${itemProps.itemData.firstName} - Last Name: ${itemProps.itemData.lastName}`
        }}
      </p>
    </template>
  </SlotFancyListChild>
</template>

<style scoped></style>
