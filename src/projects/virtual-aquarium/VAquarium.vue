<script setup>
import VFish from '@/projects/virtual-aquarium/VFish.vue'
import fishDead from '/aquarium/dead.png'
import { reactive } from 'vue'
const fishes = reactive([])

function setSunkenFish(fish) {
  let sunkenFishInterval = setInterval(() => {
    if (!fish.isLive) {
      if (fish.position.top <= 750) {
        fish.position.top += 2
        fish.style.top = `${fish.position.top}px`
      } else {
        clearInterval(sunkenFishInterval)
      }
    }
  }, 50)
}
function setFishDeadTimeout(fish) {
  setTimeout(() => {
    fish.isHungry = true
    fish.hungryTimeLeft = 5000
    setTimeout(async () => {
      if (fish.isHungry) {
        fish.img = fishDead
        fish.isLive = false
        fish.isHungry = false
        fish.hungryTimeLeft = 0
        console.log(`${fish.name} is dead! :(`)
      }
    }, fish.hungryTimeLeft)
  }, 5000)
}
function addFish(fish) {
  fish.id += fishes.length
  const reactiveFish = reactive(fish)
  fishes.push(reactiveFish)
  let positionInterval = setInterval(() => {
    if (!fish.isLive) {
      clearInterval(positionInterval)
      return
    }
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
    if (reactiveFish.position.yCurrentDirection && reactiveFish.position.top <= 700) {
      reactiveFish.position.yCurrentDirection = true
    }
    if (reactiveFish.position.yCurrentDirection && reactiveFish.position.top >= 700) {
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
  setFishDeadTimeout(reactiveFish)
  setSunkenFish(reactiveFish)
}
defineExpose({
  addFish
})

function handleFishClick(fish) {
  if (fish.isHungry) {
    fish.isHungry = false
    fish.hungryTimeLeft = 5000
    setFishDeadTimeout(fish)
  }
}
</script>

<template>
  <div class="virtual-aquarium-container">
    <VFish
      @click="handleFishClick(fish)"
      v-for="fish in fishes"
      :style="fish.style"
      :fish="fish"
      :key="fish.id"
    />
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

:deep(.fish) > label {
  padding: 0.5rem;
  background-color: rgba(0, 0, 0, 0.5);
  color: #ffffff;
}
</style>
