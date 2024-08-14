<script setup>
import fishTuna from '/aquarium/tuna.png'
import fishGoldfish from '/aquarium/goldfish.png'
import fishGoldenPurple from '/aquarium/golden-purple-fish.png'
import fishTropical from '/aquarium/tropical-fish.png'
import fishGuppies from '/aquarium/guppie.png'

import { reactive } from 'vue'
import VFish from '@/projects/virtual-aquarium/VFish.vue'

const fishes = reactive([
  { selected: false, img: fishTuna, id: 'fishTuna' },
  { selected: false, img: fishGoldfish, id: 'fishGoldfish' },
  { selected: false, img: fishGoldenPurple, id: 'fishGoldenPurple' },
  { selected: false, img: fishTropical, id: 'fishTropical' },
  { selected: false, img: fishGuppies, id: 'fishGuppies' }
])

const emit = defineEmits(['addFish'])

function handleSubmit() {
  alert('Fish added to the aquarium!')
  emit('addFish', { name: 'New Fish', img: fishTuna })
}

function handleFishClick(id) {
  fishes.map((fish) => (fish.selected = fish.id === id))
}
</script>
<template>
  <form @submit.prevent="handleSubmit">
    <div>
      <label>Select a fish:</label>
      <VFish
        :class="{ 'fish-selected': fish.selected }"
        v-for="fish in fishes"
        :key="fish.id"
        :fish="fish"
        @fish-click="handleFishClick"
      />
    </div>
    <div>
      <label for="fishName">Fish Name:</label>
      <input type="text" name="fishName" id="fishName" />
    </div>
    <button type="submit">Submit</button>
  </form>
</template>
<style scoped>
.fish-selected {
  filter: drop-shadow(2px 2px 4px rgb(85, 253, 1));
}
</style>
