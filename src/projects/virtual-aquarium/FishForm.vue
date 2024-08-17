<script setup>
import fishTuna from '/aquarium/tuna.png'
import fishGoldfish from '/aquarium/goldfish.png'
import fishGoldenPurple from '/aquarium/golden-purple-fish.png'
import fishTropical from '/aquarium/tropical-fish.png'
import fishGuppies from '/aquarium/guppie.png'

import { reactive, ref } from 'vue'
import VFish from '@/projects/virtual-aquarium/VFish.vue'

const fishName = ref('')
const fishes = reactive([
  { selected: true, img: fishTuna, id: 'fishTuna' },
  { selected: false, img: fishGoldfish, id: 'fishGoldfish' },
  { selected: false, img: fishGoldenPurple, id: 'fishGoldenPurple' },
  { selected: false, img: fishTropical, id: 'fishTropical' },
  { selected: false, img: fishGuppies, id: 'fishGuppies' }
])

const emit = defineEmits(['addFish'])

function getRandomPosition(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min
}

function handleSubmit() {
  for (const fish of fishes) {
    if (fish.selected) {
      const top = getRandomPosition(0, 750)
      const left = getRandomPosition(0, 910)

      emit('addFish', {
        isLive: true,
        isHungry: false,
        hungryTimeLeft: 0,
        name: fishName.value,
        img: fish.img,
        id: `${fish.id}`,
        position: {
          xCurrentDirection: getRandomPosition(0, 1),
          yCurrentDirection: getRandomPosition(0, 1),
          left: left,
          top: top
        },
        style: {
          position: 'absolute',
          top: `${top}px`,
          left: `${left}px`
        }
      })
      fishName.value = ''
      break
    }
  }
}

function handleFishClick(id) {
  fishes.map((fish) => (fish.selected = fish.id === id))
}
</script>
<template>
  <form @submit.prevent="handleSubmit">
    <div class="form-group">
      <label>Select a fish:</label>
      <VFish
        :class="{ 'fish-selected': fish.selected }"
        v-for="fish in fishes"
        :key="fish.id"
        :fish="fish"
        @fish-click="handleFishClick"
      />
    </div>
    <div class="form-group">
      <label for="fishName">Fish Name:</label>
      <input v-model="fishName" type="text" name="fishName" id="fishName" />
    </div>
    <button type="submit">Add Fish</button>
  </form>
</template>
<style scoped>
.fish-selected {
  filter: drop-shadow(4px 4px 8px rgb(255, 255, 255));
}

form label {
  color: #ffffff;
}

form input[type='text'] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: #ccc solid 1px;
}

form button {
  padding: 10px 20px;
  background-color: #da1c1c;
  color: white;
  border: none;
  cursor: pointer;
  width: 100%;
}

form .form-group {
  margin-bottom: 20px;
}
</style>
