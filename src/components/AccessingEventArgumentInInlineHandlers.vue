<script setup>
function warn(message, event) {
  console.log(event)
  // now we have access to the native event
  if (event) {
    event.preventDefault()
  }
  console.log(message)
}
</script>

<template>
  <button @click="(event) => warn('Using event argument', event)">
    Using event function event argument
  </button>

  <br />

  <button @click="warn('Using event argument', $event)">Using $event special variable</button>
</template>

<style scoped></style>
