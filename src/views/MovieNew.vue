<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="plot" />
        <small v-if="plot.length > 0 && plot.length < 20">{{ 20 - plot.length }} characters remaining!</small>
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="director" />
      </div>
      <div class="form-group">
        <label>English:</label>
        <input type="text" class="form-control" v-model="english" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      title: "",
      year: "",
      plot: "",
      director: "",
      english: "",
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      console.log("Creating a movie");
      var params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
        director: this.director,
        english: this.english,
      };
      axios
        .post("/api/movie", params)
        .then(() => {
          this.$router.push("/movie");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
