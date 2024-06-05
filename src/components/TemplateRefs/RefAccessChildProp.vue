<script setup>
import RefChildExposeProps from '@/components/TemplateRefs/RefChildExposeProps.vue'
import { onMounted, ref } from 'vue'

const child = ref(null)
onMounted(async () => {
  console.log(
    // refs are automatically unwrapped just like on normal instances)
    child.value.firstName
  )

  setTimeout(() => {
    child.value.firstName = 'Zapata'
  }, 5000)
})
</script>

<template>
  <RefChildExposeProps ref="child" />
</template>

<style scoped></style>
