<script setup>

import ChildEmitEvent from '@/components/Component/Emit/ChildEmitEvent.vue'

function showAlert(name) {
  alert(name)
}
</script>

<template>
  <ChildEmitEvent @show-alert="(name) => showAlert(name)" ></ChildEmitEvent>
</template>

<style scoped>

</style>