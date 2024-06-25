<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>

<template>
  <button @click="show = !show">Toggle</button>
  <!-- Example 1 -->
  <Transition v-if="false">
    <p v-if="show">hello</p>
  </Transition>

  <!-- Example 2 -->
  <Transition name="slide-fade">
    <p v-if="show">hello</p>
  </Transition>

  <!-- Example 3 -->
  <Transition name="bounce">
    <p v-if="show" style="text-align: center">Hello here is some bouncy text!</p>
  </Transition>
</template>

<style scoped>
/* Example 1 */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

/* Example 2 */
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

/* Example 3 */
.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
</style>
