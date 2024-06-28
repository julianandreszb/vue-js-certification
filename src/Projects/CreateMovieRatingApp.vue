<script setup>
import { StarIcon } from '@heroicons/vue/24/solid'
import { items } from './movies.json'
import { ref } from 'vue'

// 1. Define the movies as reactive data.
const movies = ref(items)

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
</script>

<template>
  <!-- This is where your template goes	-->
  <div>
    <!-- 2. Use the Vue.js template syntax to display the movie information. -->
    <section class="cards-container">
      <article v-for="movie in movies" :key="movie.id" class="card">
        <div class="start-icon-container" :class="{ active: movie.rating > 0 }">
          <StarIcon /><span>{{ movie.rating }}</span>
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
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 2rem;
  box-sizing: border-box;
  background-color: #000;
  height: 100vh;
  width: 100vw;
}
p {
  margin: 0;
}
</style>

<style scoped>
.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
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
</style>
