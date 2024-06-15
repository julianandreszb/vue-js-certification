<script setup>
import { ref } from 'vue'
const props = defineProps({
  loadingTimeout: {
    type: Number,
    default: 1000
  }
})
const items = ref([])

setTimeout(() => {
  items.value = [
    {
      id: 1,
      firstName: 'Julian',
      lastName: 'Zapata'
    },
    {
      id: 2,
      firstName: 'Ian',
      lastName: 'Zapata'
    },
    {
      id: 3,
      firstName: 'Hellen',
      lastName: 'Patino'
    }
  ]
}, props.loadingTimeout)
</script>

<template>
  <div v-if="!items.length">
    <p>Loading...</p>
  </div>
  <ul v-else>
    <li v-for="item in items" :key="item.id">
      <slot name="item" :itemData="item"></slot>
    </li>
  </ul>
</template>

<style scoped></style>
