<script setup>

</script>

<template>
  <h1 v-if="$slots.headerOne" >
    <slot name="headerOne">Default headerOne Content</slot>
  </h1>
  <h2 v-if="$slots.headerTwo" >
    <slot name="headerTwo" >Default headerTwo Content</slot>
  </h2>
</template>

<style scoped>

</style>