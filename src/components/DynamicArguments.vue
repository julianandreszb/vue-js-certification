<script setup>
const attributeRefValue = 'https://www.google.com'
const attributeRef = 'href'
const attributeTarget = 'target'
const attributeTargetValue = '_blank'
</script>

<template>
  <a v-bind:[attributeRef]="attributeRefValue" v-bind:[attributeTarget]="attributeTargetValue" >It should open Google in a new tab!</a>
</template>

<style scoped></style>