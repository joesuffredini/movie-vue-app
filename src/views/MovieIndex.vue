<template>
  <div class="movie">
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <!-- <p>{{ movie.year }}</p>
        <p>{{ movie.plot }}</p>
        <p>{{ movie.director }}</p> -->
        <router-link v-bind:to="`movie/${movie.id}`">
          <h3>{{ movie.title }}</h3>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.MovieIndex();
  },
  methods: {
    MovieIndex: function () {
      axios.get("/api/movie/").then((response) => {
        this.movies = response.data;
        console.log("all movies:", this.movies);
      });
    },
  },
};
</script>
