<script setup>
import { ref } from 'vue'

const theLastName = ref('Zapata')
</script>

<template>
  <div>
    <slot :firstName="`Julian`" :lastName="theLastName"></slot>
    <button @click="() => (theLastName = 'LastName was changed :D')">
      Change LastName from child
    </button>
  </div>
</template>

<style scoped></style>
