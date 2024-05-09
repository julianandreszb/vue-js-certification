<script setup>
import { reactive } from 'vue'

const objectOfAttributes = reactive({
  value: 'Hello World', // value attribute is not bind to the input element
  class: 'text-red',
  id: 'unique-id',
})

</script>

<template>
  <input v-bind="objectOfAttributes" />
  <!-- RENDER:  -->
  <!-- <input class="text-red" id="unique-id">  -->
  
  
  <!-- SAME THAT -->
  <input :value="objectOfAttributes.value" :class="objectOfAttributes.class" :id="objectOfAttributes.id" />
  <!-- RENDER:  -->
  <!-- <input class="text-red" id="unique-id">  -->
  
  
  <!-- SAME THAT -->
  <input v-bind:value="objectOfAttributes.value" v-bind:class="objectOfAttributes.class" v-bind:id="objectOfAttributes.id" />
  <!-- RENDER:  -->
  <!-- <input class="text-red" id="unique-id">  -->
</template>

<style scoped>
.text-red {
  color: red;
}
</style>