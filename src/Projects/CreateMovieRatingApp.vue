<script setup>
import { items } from './movies.json'
import { ref } from 'vue'
// 1. Define the movies as reactive data.
const movies = ref(items)

/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/
// import { StarIcon } from "@heroicons/vue/24/solid";
</script>

<template>
  <!-- This is where your template goes	-->
  <div>
    <!-- 2. Use the Vue.js template syntax to display the movie information. -->
    <section class="cards-container">
      <article v-for="movie in movies" :key="movie.id" class="card">
        <img class="card-img" :src="movie.image" :alt="movie.description" />
        <div class="card-content">
          <h2 class="card-header">{{ movie.name }}</h2>
          <ul class="card-badges">
            <li class="card-badge" v-for="genre in movie.genres" :key="genre">{{ genre }}</li>
          </ul>
          <p>{{ movie.description }}</p>
          <div class="spacer-x1"></div>
          <div class="card-rating">
            <span>Rating: ({{ movie.rating }}/5) </span>
            <span v-for="_ in movie.rating">⭐️</span>
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
}

.card-content {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.card-header {
  font-weight: bold;
  font-size: 1.2rem;
}

.card-badges {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 10px;
  list-style: none;
  padding: 0;
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
}

.card-rating {
  display: flex;
  flex-direction: row;
  gap: 6px;
}
.spacer-x1 {
  height: 10px;
}
</style>
