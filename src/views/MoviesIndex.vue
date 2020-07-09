<template>
  <div class="movies-index">
    
    <div v-for="movie in movies">
      <h2>{{ movie.title }} ({{ movie.year }})</h2>
      <h4>Director: {{ movie.director }}</h4>
      <p>{{ movie.plot }}</p>
      <router-link class="nav-link" :to="`/movies/${movie.id}`">More Info</router-link>
    </div>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: []
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        this.movies = response.data;
      });
    }
  }
};
</script>
