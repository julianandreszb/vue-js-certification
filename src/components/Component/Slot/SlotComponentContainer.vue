<script setup>
import SlotChild from '@/components/Component/Slot/SlotChild.vue'
import SlotChildDefaultValue from '@/components/Component/Slot/SlotChildDefaultValue.vue'
import SlotChildNamedSlots from '@/components/Component/Slot/SlotChildNamedSlots.vue'
import SlotConditionalSlots from '@/components/Component/Slot/SlotConditionalSlots.vue'
import SlotDynamicSlotNames from '@/components/Component/Slot/SlotDynamicSlotNames.vue'
import { ref } from 'vue'
const currentSlot = ref('headerOne')
function toggleSlot(){
  currentSlot.value = currentSlot.value === 'headerOne' ? 'headerTwo' : 'headerOne';
}
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
    <template v-slot:title><h1>This is the title slot. Using v-slot:title</h1></template>
    <template #body><p>This is the content slot. Using #body</p></template>
  </SlotChildNamedSlots>
  
  <hr>
  <p>Conditional Slots</p>
  <SlotConditionalSlots/>
  <SlotConditionalSlots>
    <template v-slot:header>
      Header (Just header slot was provided)
    </template>
  </SlotConditionalSlots>
  <SlotConditionalSlots>
    <template v-slot:header>
      Header (Just header and body slot were provided)
    </template>
    <template v-slot:body>
      This is the body
    </template>
  </SlotConditionalSlots>
  <SlotConditionalSlots>
    <template v-slot:header>
      Header (All slots were provided (header, body and footer))
    </template>
    <template v-slot:body>
      This is the body
    </template>
    <template v-slot:footer>
      This is the footer
    </template>
  </SlotConditionalSlots>

  <hr>
  <p>Dynamic slots</p>
  <SlotDynamicSlotNames>
    <template #[currentSlot]>{{ currentSlot === 'headerOne' ? 'Header one' : 'Header two' }}</template>  
  </SlotDynamicSlotNames>
  <button @click="toggleSlot" >Toggle dynamic slot (headerOne, headerTwo)</button>
</template>

<style scoped></style>
