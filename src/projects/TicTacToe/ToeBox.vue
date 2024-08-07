<script setup>
import { ref } from 'vue'

const props = defineProps({
  box: {
    type: Object,
    required: true
  },
  currentPlayer: {
    type: String,
    required: true
  }
})
const emit = defineEmits(['updateBox'])

const boxValue = ref('')

function handleUserSelect() {
  if (boxValue.value) {
    return
  }
  boxValue.value = props.currentPlayer
  emit('updateBox', props.box)
}
</script>

<template>
  <div @click="handleUserSelect" class="box">{{ boxValue }}</div>
</template>

<style scoped>
.box {
  cursor: pointer;
  user-select: none;
}
</style>
