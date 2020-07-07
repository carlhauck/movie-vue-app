<template>
  <div class="home">
    <h1>Flixx</h1>
    <div>
      Title: <input type="text" v-model="title"><br>
      Year: <input type="text" v-model="year"><br>
      Director: <input type="text" v-model="director"><br>
      Plot: <input type="text" v-model="plot"><br>
      <button v-on:click="createMovie()">Create Movie</button>
      <p v-for="error in errors">{{ error }}</p>
    </div>
    <div v-for="movie in movies">
      <h2>{{ movie.title }} ({{ movie.year }})</h2>
      <p>Director: {{ movie.director }}</p>
      <p>{{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">Edit Movie</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Edit Movie</h1>
        <p>Title: <input type="text" v-model="currentMovie.title"></p>
        <p>Year: <input type="text" v-model="currentMovie.year"></p>
        <p>Director: <input type="text" v-model="currentMovie.director"></p>
        <p>Plot: <input type="text" v-model="currentMovie.plot"></p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">Delete</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: [],
      title: "",
      year: "",
      director: "",
      plot: "",
      currentMovie: [],
      errors: []
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log("All Movies:", response.data);
        this.movies = response.data;
      });
    },
    createMovie: function() {
      var params = {
        title: this.title,
        year: this.year,
        director: this.director,
        plot: this.plot
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
      this.title = "";
      this.year = "";
      this.director = "";
      this.plot = "";
    },
    showMovie: function(movie) {
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        director: movie.director,
        plot: movie.plot
      };
      axios.patch(`/api/movies/${movie.id}`, params);
    },
    destroyMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`);
      var index = this.movies.indexOf(movie);
      this.movies.splice(index, 1);
    }
  }
};
</script>