<template>
  <div class="movies-new">

    <form v-on:submit.prevent="createMovie()">
      <h1>Create Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="year">
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="director">
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="plot">
        <small v-show="plot.length > 0 && plot.length <= 200">{{ 200 - plot.length }} characters remaining</small>
        <small class = "text-danger" v-show="plot.length > 200">{{ plot.length - 200 }} characters over limit</small>
      </div>
      <input type="submit" class="btn btn-primary" value="Create">
    </form>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      errors: [],
      title: "",
      year: "",
      director: "",
      plot: ""
    };
  },
  created: function() {},
  methods: {
    createMovie: function() {
      var params = {
        title: this.title,
        year: this.year,
        director: this.director,
        plot: this.plot
      };
      axios
        .post(`/api/movies/`, params)
        .then(response => {
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>