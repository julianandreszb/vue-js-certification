<script setup>
import { PencilIcon, StarIcon, TrashIcon } from '@heroicons/vue/24/solid/index.js'

const emits = defineEmits(['delete', 'edit', 'update:rating'])

const props = defineProps({
  movie: {
    type: Object,
    required: true
  }
})

function isStartActive(rating, ratingIndex) {
  return ratingIndex <= rating
}

function deleteMovie() {
  emits('delete', props.movie.id)
}
function editMovie() {
  emits('edit', props.movie.id)
}
function updateRating(rating) {
  emits('update:rating', props.movie.id, rating)
}
</script>

<template>
  <article :key="props.movie.id" class="card">
    <div class="start-icon-container" :class="{ active: props.movie.rating > 0 }">
      <StarIcon />
      <span>{{ props.movie.rating }}</span>
    </div>
    <img class="card-img" :src="props.movie.image" :alt="props.movie.description" />
    <div class="card-content">
      <h2 class="card-header">{{ props.movie.name }}</h2>
      <ul class="card-badges">
        <li class="card-badge" v-for="genre in props.movie.genres" :key="genre">{{ genre }}</li>
      </ul>
      <div class="movie-description-container">
        <p>{{ props.movie.description }}</p>
      </div>
      <div class="card-footer">
        <div class="card-rating">
          <span>Rating: ({{ props.movie.rating }}/5) </span>
          <StarIcon
            @click="updateRating(ratingValue)"
            class="icon star-rating"
            :class="{ active: isStartActive(props.movie.rating, ratingValue) }"
            v-for="ratingValue in 5"
            :key="ratingValue"
          ></StarIcon>
        </div>
        <div class="card-actions">
          <span @click="deleteMovie()" class="card-icon-container"
            ><TrashIcon class="icon card-icon-action"></TrashIcon
          ></span>
          <span class="card-icon-container" @click="editMovie"
            ><PencilIcon class="icon card-icon-action"></PencilIcon
          ></span>
        </div>
      </div>
    </div>
  </article>
</template>

<style scoped>
.card {
  background-color: #fff;
  border-radius: 4px;
  text-align: left;
  position: relative;
}

.card-content {
  position: relative;
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 6px;
  height: 240px;

  p {
    margin-top: 6px;
  }
}

.card-header {
  font-weight: bold;
  font-size: 1.2rem;
  margin: 0;
}

.card-badges {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 10px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.card-badge {
  background-color: rebeccapurple;
  padding-inline: 6px;
  color: #fff;
  border-radius: 8px;
}

.card-img {
  width: 100%;
  aspect-ratio: 9 / 16;
  object-fit: cover;
  margin-bottom: 20px;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}

.card-footer {
  display: flex;
  flex-direction: row;
  gap: 6px;
  margin-top: auto;
  width: 100%;
  justify-content: space-between;
}

.icon {
  cursor: pointer;
  height: 20px;
  width: 20px;
}

.star-rating.active {
  color: #f5ad01;
}

.star-rating:hover {
  cursor: pointer;
}

.start-icon-container {
  position: absolute;
  top: 4px;
  right: 4px;
  height: 40px;
  width: 40px;
  color: #dedede;

  span {
    position: absolute;
    color: #000000;
    left: 16px;
    top: 12px;
  }
}

.start-icon-container.active {
  color: #f5ad01;
}

.movie-description-container {
  height: 6rem;
  overflow: scroll;
}

.card-actions {
  display: flex;
  flex-direction: row;
  gap: 0.5rem;
  align-items: center;
}

.card-icon-action {
  padding: 0.5rem;
  border-radius: 100%;
  background-color: #c2cad8;
}

.card-icon-action:hover {
  background-color: #8a9194;
}

.card-rating {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.card-icon-container {
  display: contents;
}
</style>
