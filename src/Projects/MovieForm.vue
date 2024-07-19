<script setup>
import { nextTick, onMounted, ref } from 'vue'

const props = defineProps({
  modelValue: {
    type: Object
  }
})
const movieNameRef = ref(null)
onMounted(() => movieNameRef.value.focus())

const emit = defineEmits(['update:modelValue', 'cancel'])
</script>

<template>
  <form class="form-add-movie" @submit.prevent="() => emit('update:modelValue', props.modelValue)">
    <div class="field-group">
      <label for="name">Name</label>
      <input ref="movieNameRef" v-model="props.modelValue.name" type="text" name="name" />
    </div>
    <div class="field-group">
      <label for="description">Description</label>
      <textarea v-model="props.modelValue.description" name="description"></textarea>
    </div>
    <div class="field-group">
      <label for="image">Image</label>
      <input v-model="props.modelValue.image" type="text" name="image" />
    </div>
    <div class="field-group">
      <label for="genres">Genres</label>
      <select v-model="props.modelValue.genres" name="genres" multiple>
        <option value="Action">Action</option>
        <option value="Comedy">Comedy</option>
        <option value="Drama">Drama</option>
        <option value="Horror">Horror</option>
        <option value="Romance">Romance</option>
      </select>
    </div>
    <div class="field-group field-checkbox">
      <input
        v-model="props.modelValue.inTheaters"
        type="checkbox"
        name="in_theater"
        id="in_theater"
      />
      <label for="in_theater">In Theaters</label>
    </div>
    <div class="field-group-actions">
      <button @click="emit('cancel')" class="btn btn-cancel" type="button">Cancel</button>

      <button class="btn btn-submit" type="submit">
        <span v-if="props.modelValue.id">Edit</span><span v-else>Submit</span>
      </button>
    </div>
  </form>
</template>

<style scoped>
.form-add-movie {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  background-color: #1c1c1c;
  width: 400px;
  padding: 1rem;
  height: 400px;
}

label,
input,
textarea {
  color: #ffffff;
  display: block;
  border: none;
}

input,
textarea {
  background-color: #000000;
}

.field-group {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.field-group.field-checkbox {
  display: flex;
  flex-direction: row;
  align-content: start;
}

.field-group-actions {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  gap: 1rem;
}

.btn-cancel {
  background-color: #5b6773;
  color: white;
}
.btn-cancel:hover {
  background-color: #8293a4;
  color: white;
}
</style>
