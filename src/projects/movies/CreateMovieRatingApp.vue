<script setup>
import { items } from './movies.json'
import { computed, defineAsyncComponent, reactive, ref } from 'vue'
import MovieItem from '@/projects/movies/components/MovieItem.vue'
const MovieForm = defineAsyncComponent(() => import('@/projects/movies/components/MovieForm.vue'))
const AppModal = defineAsyncComponent(() => import('@/projects/movies/components/AppModal.vue'))

// 1. Define the movies as reactive data.
const movies = ref(items)
const isModalOpen = ref(false)
const form = reactive({
  id: '',
  name: '',
  description: '',
  image: '',
  genres: [],
  rating: 0,
  inTheaters: false
})

function clearForm() {
  form.id = ''
  form.name = ''
  form.description = ''
  form.image = ''
  form.genres = []
  form.rating = 0
  form.inTheaters = false
}

function isMovieValid(movie) {
  const isValid = movie.name && movie.description && movie.image && movie.genres.length > 0
  if (!isValid) {
    console.log('Movie is not valid', movie)
  }
  return isValid
}

function showDialog() {
  isModalOpen.value = true
}

function hideDialog() {
  isModalOpen.value = false
}

function createMovie() {
  if (!isMovieValid(form)) {
    return
  }
  form.id = Math.random().toString(36).substring(2, 9) // Generate a unique ID for the movie.
  movies.value.push(JSON.parse(JSON.stringify(form)))
  hideDialog()
}

function updateMovie() {
  if (!isMovieValid(form)) {
    return
  }
  movies.value = movies.value.map((movie) => {
    if (movie.id === form.id) {
      movie.name = form.name
      movie.description = form.description
      movie.image = form.image
      movie.genres = form.genres
      movie.inTheaters = form.inTheaters
      movie.rating = form.rating
    }
    return movie
  })
  hideDialog()
}

function startCreateMovieProcess() {
  clearForm()
  showDialog()
}

function editMovie(id) {
  const movie = movies.value.find((movie) => movie.id === id)

  form.id = movie.id
  form.name = movie.name
  form.description = movie.description
  form.image = movie.image
  form.genres = movie.genres
  form.inTheaters = movie.inTheaters
  form.rating = movie.rating
  showDialog()
}

function deleteMovie(id) {
  movies.value = movies.value.filter((currentMovie) => currentMovie.id !== id)
}

const averageRating = computed(() => {
  if (movies.value.length) {
    const totalRatings = movies.value.reduce((sum, movie) => sum + movie.rating, 0)
    return totalRatings / movies.value.length
  }
  return 0
})

function startResetRatings() {
  movies.value.forEach((movie) => {
    movie.rating = 0
  })
}

function setMovieRating(id, ratingValue) {
  movies.value = movies.value.map((movie) => {
    if (movie.id === id) {
      movie.rating = ratingValue
    }
    return movie
  })
}

function saveMovie(form) {
  if (form.id !== '') {
    updateMovie()
  } else {
    createMovie()
  }
}
</script>

<template>
  <!-- This is where your template goes	-->
  <div class="container">
    <section class="options-container">
      <div>
        <p class="movies-summary">
          Total Movies: {{ movies.length }} / Average Rating: {{ averageRating }}
        </p>
      </div>
      <div class="movies-actions">
        <button type="button" class="btn btn-submit" @click="startResetRatings">
          Remove Ratings
        </button>
        <button type="button" class="btn btn-submit" @click="startCreateMovieProcess">
          Add Movie
        </button>
      </div>
    </section>

    <!-- 2. Use the Vue.js template syntax to display the movie information. -->
    <section class="cards-container">
      <MovieItem
        v-for="movieVal in movies"
        :key="movieVal.id"
        :movie="movieVal"
        @delete="deleteMovie"
        @edit="editMovie"
        @update:rating="setMovieRating"
      />
    </section>

    <AppModal
      :show="isModalOpen"
      @close="hideDialog"
      :title="form.id ? 'Edit Movie' : 'Save Movie'"
    >
      <MovieForm @cancel="hideDialog" @update:modelValue="saveMovie" :model-value="form" />
    </AppModal>
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
  justify-content: space-between;
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

.btn {
  border-radius: 8px;
  padding-inline: 0.5rem;
  padding-block: 0.5rem;
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
</style>

<style scoped>
.cards-container {
  padding-inline: 1rem;
  padding-block: 1rem;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-gap: 20px;
}

.movies-summary {
  font-size: 1.2rem;
  color: #fff;
  font-weight: bold;
}

.movies-actions {
  display: flex;
  flex-direction: row;
  gap: 1rem;
}
</style>
