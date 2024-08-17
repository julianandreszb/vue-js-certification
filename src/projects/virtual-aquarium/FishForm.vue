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

function handleSubmit() {
  for (const fish of fishes) {
    if (fish.selected) {
      emit('addFish', {
        name: fishName.value,
        img: fish.img,
        id: `${fish.id}`,
        position: {
          xCurrentDirection: 1,
          yCurrentDirection: 1,
          left: 0,
          top: 0
        },
        style: {
          position: 'absolute',
          top: '50px',
          left: '50px'
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
