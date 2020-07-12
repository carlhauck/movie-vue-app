<template>

  <div class="movies-index">
    Search by title: <input v-model="titleFilter" list="titles">
    <datalist id="titles">
      <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')">
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: ""
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
