<script setup>
const props = defineProps({
  title: {
    type: String,
    default: null
  },
  show: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['close'])
</script>

<template>
  <transition>
    <article v-if="show" class="overlay">
      <div class="modal-content-wrap">
        <h2 class="modal-title">{{ props.title }}</h2>
        <span @click="emit('close')" class="close-button">×</span>
        <slot />
      </div>
    </article>
  </transition>
</template>

<style scoped>
.modal-content-wrap {
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal-title {
  margin: 0;
  background-color: #1c1c1c;
  color: #ffffff;
  padding: 1rem;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5); /* semi-transparent background */
  backdrop-filter: blur(5px); /* apply blur effect */
}

.close-button {
  background-color: transparent;
  color: white;
  font-size: 2rem;
  position: absolute;
  right: 1rem;
  top: 0;
}

.close-button:hover {
  cursor: pointer;
  color: lightgray;
}

.v-enter-active,
.v-leave-active,
.v-enter-active .modal-content-wrap,
.v-leave-active .modal-content-wrap {
  transition: all 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.v-enter-from .modal-content-wrap,
.v-leave-to .modal-content-wrap {
  transform: translateY(-50px);
}
</style>
