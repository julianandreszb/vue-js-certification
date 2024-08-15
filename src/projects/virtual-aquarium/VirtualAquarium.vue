<script setup>
import FishForm from '@/projects/virtual-aquarium/FishForm.vue'
import VAquarium from '@/projects/virtual-aquarium/VAquarium.vue'
</script>

<template>
  <article class="container">
    <section class="section-container">
      <FishForm />
    </section>
    <section>
      <VAquarium />
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
