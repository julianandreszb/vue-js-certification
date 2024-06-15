<script setup>

</script>

<template>
<div class="card" >
  <h1 v-if="$slots.header" >
    <slot name="header"></slot>
  </h1>
  <p v-if="$slots.body" >
    <slot name="body"></slot>
  </p>
  <p v-if="$slots.footer" >
    <slot name="footer"></slot>
  </p>
</div>
</template>

<style scoped>
.card {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  background-color: tomato;
  margin-block-end: 2rem;
  
  h1 {
    color: white;
    text-align: center;
    font-size: 1rem;
  }
  
  p {
    color: white;
    text-align: center;
    font-size: 1rem;
  }
}

</style>