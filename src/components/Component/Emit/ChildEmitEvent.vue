<script setup>
const emit = defineEmits([])
</script>

<template>
 <button @click="$emit('show-alert', 'Julian (Using $emit)')" >Emit Alert Using $emit</button>
 <button @click="emit('show-alert', 'Julian (Using defineEmits)')" >Emit Alert Using defineEmites</button>
</template>

<style scoped>

</style>