<template>
  <div class="home">
    <h1>The Movie App</h1>

    <!-- !-- Create Button -->
    <div>
      <h2>Create New Movies for the Database</h2>
      Title:
      <input type="text" v-model="newMovieTitle" />
      <br />
      Year:
      <input type="text" v-model="newMovieYear" />
      <br />
      Plot:
      <input type="text" v-model="newMoviePlot" />
      <br />
      Director:
      <br />
      <input type="text" v-model="newMovieDirector" />
      <br />
    </div>

    <br />
    <br />
    <button v-on:click="createMovie()">Create</button>
    <br />
    <br />

    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <p>{{ movie.title }}</p>
        <!-- <p>{{ movie.plot }}</p>
        <p>{{ movie.year }}</p>
        <p>{{ movie.director }}</p> -->
        <!-- <br /> -->
        <button v-on:click="showMovie(movie)">Click for more info</button>
        <!-- <br /> -->
      </div>

      <!-- Modal  -->

      <dialog id="movie-details">
        <form method="dialog">
          <h1>Product info</h1>
          <p>
            Name:
            <input type="text" v-model="currentMovie.title" />
          </p>
          <br />
          <p>
            Description:
            <input type="text" v-model="currentMovie.plot" />
          </p>
          <p>
            Plot:
            <input type="text" v-model="currentMovie.year" />
          </p>
          Director:
          <input type="text" v-model="currentMovie.director" />
          <p>
            <br />
            <button v-on:click="updateMovie(currentMovie)">Update</button>
            <button v-on:click="deleteMovie(currentMovie)">Delete</button>
            <button>Exit</button>
          </p>
        </form>
      </dialog>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      currentMovie: {},
    };
  },

  created: function () {
    this.indexMovies();
  },

  methods: {
    indexMovies: function () {
      axios.get("/api/movie").then((response) => {
        this.movies = response.data;
        console.log(this.movies);
      });
    },
    createMovie: function () {
      console.log("Create Movie");
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
      };
      axios.post("/api/movie", params).then((response) => {
        console.log(response.data);
        this.movies.push(response.data);
      });
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
      };
      axios.patch("/api/movie/" + movie.id, params).then((response) => {
        console.log("Success", response.data);
      });
    },
    deleteMovie: function (movie) {
      axios.delete("/api/movie/" + movie.id).then((response) => {
        console.log("Success!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
