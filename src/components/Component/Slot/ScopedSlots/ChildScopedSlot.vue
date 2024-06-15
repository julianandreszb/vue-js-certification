<script setup>
import { ref } from 'vue'

const theLastName = ref('Zapata')
</script>

<template>
  <div>
    <slot :firstName="`Julian`" :lastName="theLastName"></slot>
    <button
      @click="() => (theLastName = 'LastName was changed :D')"
      :style="{ marginBottom: '1rem' }"
    >
      Change LastName from child
    </button>
    <br />
    <slot v-if="$slots.address" name="address" :addressOne="`Street 123`"></slot>
  </div>
</template>

<style scoped></style>
