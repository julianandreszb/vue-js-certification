<script setup>
import FishForm from '@/projects/virtual-aquarium/FishForm.vue'
import VAquarium from '@/projects/virtual-aquarium/VAquarium.vue'
import { ref } from 'vue'
const aquarium = ref(null)
function addFishListener(fish) {
  aquarium.value && aquarium.value.addFish(fish)
}
</script>

<template>
  <article class="container">
    <section class="section-container">
      <FishForm @addFish="addFishListener" />
    </section>
    <section>
      <VAquarium ref="aquarium" />
    </section>
  </article>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
}
.section-container {
  padding: 1rem;
  background-color: #1f407b;
}
</style>
