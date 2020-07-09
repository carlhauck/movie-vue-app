<template>
  <div class="movies-show">
    <h2>{{ movie.title }} ({{ movie.year }})</h2>
    <h4>Director: {{ movie.director }}</h4>
    <p>{{ movie.plot }}</p>
    <router-link class="nav-link" :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function() {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/api/movies/${this.$route.params.id}`).then(response => {
          this.$router.push("/movies");
        });
      }
    }
  }
};
</script>