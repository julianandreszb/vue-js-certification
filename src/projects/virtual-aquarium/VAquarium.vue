<script setup>
import VFish from '@/projects/virtual-aquarium/VFish.vue'
import fishGuppies from '/aquarium/guppie.png'
import { reactive } from 'vue'
const fish = reactive({
  img: fishGuppies,
  id: 'Guppies1',
  position: {
    xCurrentDirection: 1,
    yCurrentDirection: 1,
    left: 0
  }
})
const fishStyle = reactive({
  position: 'absolute',
  top: '50px',
  left: '50px'
})

setInterval(() => {
  // 1: right
  // 0: left
  if (fish.position.xCurrentDirection && fish.position.left <= 910) {
    fish.position.xCurrentDirection = true
  }
  if (fish.position.xCurrentDirection && fish.position.left >= 910) {
    fish.position.xCurrentDirection = false
  }
  if (!fish.position.xCurrentDirection && fish.position.left >= 0) {
    fish.position.xCurrentDirection = false
  }
  if (!fish.position.xCurrentDirection && fish.position.left <= 0) {
    fish.position.xCurrentDirection = true
  }

  fish.position.left = fish.position.xCurrentDirection
    ? (fish.position.left += 10)
    : (fish.position.left -= 10)

  fishStyle.left = `${fish.position.left}px`
  fishStyle.transform = fish.position.xCurrentDirection ? 'scaleX(1)' : 'scaleX(-1)'
}, 50)
</script>

<template>
  <div class="virtual-aquarium-container">
    <VFish :style="fishStyle" :fish="fish" />
  </div>
</template>

<style scoped>
.virtual-aquarium-container {
  position: relative;
  width: 1000px;
  height: 800px;
  background-image: url('/aquarium/bg.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}
</style>
