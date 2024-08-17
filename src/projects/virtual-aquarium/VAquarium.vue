<script setup>
import VFish from '@/projects/virtual-aquarium/VFish.vue'
import { reactive } from 'vue'
const fishes = reactive([])

function addFish(fish) {
  console.log(`addFish: `, fish)
  fish.id += fishes.length
  const reactiveFish = reactive(fish)
  fishes.push(reactiveFish)
  setInterval(() => {
    // Update left position
    // 1: right
    // 0: left
    if (reactiveFish.position.xCurrentDirection && reactiveFish.position.left <= 910) {
      reactiveFish.position.xCurrentDirection = true
    }
    if (reactiveFish.position.xCurrentDirection && reactiveFish.position.left >= 910) {
      reactiveFish.position.xCurrentDirection = false
    }
    if (!reactiveFish.position.xCurrentDirection && reactiveFish.position.left >= 0) {
      reactiveFish.position.xCurrentDirection = false
    }
    if (!reactiveFish.position.xCurrentDirection && reactiveFish.position.left <= 0) {
      reactiveFish.position.xCurrentDirection = true
    }

    reactiveFish.position.left = reactiveFish.position.xCurrentDirection
      ? (reactiveFish.position.left += 2)
      : (reactiveFish.position.left -= 2)

    reactiveFish.style.left = `${reactiveFish.position.left}px`
    reactiveFish.style.transform = reactiveFish.position.xCurrentDirection
      ? 'scaleX(1)'
      : 'scaleX(-1)'

    // Update top position
    // 1: down
    // 0: up
    if (reactiveFish.position.yCurrentDirection && reactiveFish.position.top <= 750) {
      reactiveFish.position.yCurrentDirection = true
    }
    if (reactiveFish.position.yCurrentDirection && reactiveFish.position.top >= 750) {
      reactiveFish.position.yCurrentDirection = false
    }
    if (!reactiveFish.position.yCurrentDirection && reactiveFish.position.top >= 0) {
      reactiveFish.position.yCurrentDirection = false
    }
    if (!reactiveFish.position.yCurrentDirection && reactiveFish.position.top <= 0) {
      reactiveFish.position.yCurrentDirection = true
    }

    reactiveFish.position.top = reactiveFish.position.yCurrentDirection
      ? (reactiveFish.position.top += 2)
      : (reactiveFish.position.top -= 2)

    reactiveFish.style.top = `${reactiveFish.position.top}px`
  }, 50)
}
defineExpose({
  addFish
})
</script>

<template>
  <div class="virtual-aquarium-container">
    <VFish v-for="fish in fishes" :style="fish.style" :fish="fish" :key="fish.id" />
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
