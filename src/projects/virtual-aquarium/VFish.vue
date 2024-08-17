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
    <p class="fish-message" v-if="props.fish.isHungry">Feed me!</p>
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

.fish-message {
  background-color: #ffffff;
  color: #000000;
}
</style>
