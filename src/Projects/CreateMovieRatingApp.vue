<script setup>
import { StarIcon } from '@heroicons/vue/24/solid'
import { items } from './movies.json'
import { reactive, ref } from 'vue'

// 1. Define the movies as reactive data.
const movies = ref(items)
const isCreateMovieDialogOpen = ref(false)
const movie = reactive({
  name: '',
  description: '',
  image: '',
  genres: [],
  rating: 0,
  inTheaters: false
})

/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/
function setMovieRating(movie, ratingValue) {
  if (movie.rating === ratingValue) {
    return
  }
  movie.rating = ratingValue
}

function isStartActive(rating, ratingIndex) {
  return ratingIndex <= rating
}

function createMovie(movie) {}
</script>

<template>
  <!-- This is where your template goes	-->
  <div class="container">
    <section class="options-container">
      <button @click="isCreateMovieDialogOpen = !isCreateMovieDialogOpen">Add Movie</button>
    </section>

    <!-- 2. Use the Vue.js template syntax to display the movie information. -->
    <section class="cards-container">
      <article v-for="movie in movies" :key="movie.id" class="card">
        <div class="start-icon-container" :class="{ active: movie.rating > 0 }">
          <StarIcon />
          <span>{{ movie.rating }}</span>
        </div>
        <img class="card-img" :src="movie.image" :alt="movie.description" />
        <div class="card-content">
          <h2 class="card-header">{{ movie.name }}</h2>
          <ul class="card-badges">
            <li class="card-badge" v-for="genre in movie.genres" :key="genre">{{ genre }}</li>
          </ul>
          <p>{{ movie.description }}</p>
          <div class="card-rating">
            <span>Rating: ({{ movie.rating }}/5) </span>
            <StarIcon
              @click="setMovieRating(movie, ratingValue)"
              class="star-rating"
              :class="{ active: isStartActive(movie.rating, ratingValue) }"
              v-for="ratingValue in 5"
              :key="ratingValue"
            ></StarIcon>
          </div>
        </div>
      </article>
    </section>

    <article v-if="isCreateMovieDialogOpen" class="overlay">
      <form action="" class="form-add-movie">
        <div class="field-group">
          <label for="name">Name</label>
          <input v-model="movie.name" type="text" name="name" />
        </div>
        <div class="field-group">
          <label for="description">Description</label>
          <textarea v-model="movie.description" name="description"></textarea>
        </div>
        <div class="field-group">
          <label for="image">Image</label>
          <input v-model="movie.image" type="text" name="image" />
        </div>
        <div class="field-group">
          <label for="genres">Genres</label>
          <select v-model="movie.genres" name="genres" multiple>
            <option value="Action">Action</option>
            <option value="Comedy">Comedy</option>
            <option value="Drama">Drama</option>
            <option value="Horror">Horror</option>
            <option value="Romance">Romance</option>
          </select>
        </div>
        <div class="field-group field-checkbox">
          <input v-model="movie.inTheaters" type="checkbox" name="in_theater" id="in_theater" />
          <label for="in_theater">In Theaters</label>
        </div>
        <div class="field-group-actions">
          <button
            @click="isCreateMovieDialogOpen = !isCreateMovieDialogOpen"
            class="btn btn-cancel"
            type="button"
          >
            Cancel
          </button>
          <button @click.prevent="createMovie" class="btn btn-submit" type="submit">Create</button>
        </div>
      </form>
    </article>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
}

.options-container {
  padding-block: 1rem;
  padding-inline: 1rem;
  display: flex;
  flex-direction: row;
  justify-content: end;
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: #000;
  height: 100vh;
  width: 100vw;

  font-family: Roboto, sans-serif;
}

p {
  margin: 0;
}
</style>

<style scoped>
.cards-container {
  padding-inline: 1rem;
  padding-block: 1rem;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 20px;
}

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

.card-rating {
  position: absolute;
  bottom: 1rem;
  display: flex;
  flex-direction: row;
  gap: 6px;
  margin-top: auto;
}

.star-rating {
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

  button {
    border-radius: 8px;
    padding-inline: 0.5rem;
    padding-block: 0.5rem;
  }
}

.btn {
  border: none;
  cursor: pointer;
}

.btn-submit {
  background-color: #3ba9c9;
  color: white;
}

.btn-submit:hover {
  background-color: #48ccf3;
  color: white;
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
