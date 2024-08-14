<script setup>
const props = defineProps({
  fish: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['fishClick'])
</script>

<template>
  <div class="fish" @click="emit('fishClick', props.fish.id)">
    <img :src="props.fish.img" alt="Fish" />
    <label>{{ props.fish.name }}</label>
  </div>
</template>

<style scoped>
.fish {
  cursor: pointer;
}
.fish img {
  width: 5rem;
}
</style>
