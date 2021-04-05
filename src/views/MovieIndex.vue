<template>
  <div class="movie">
    <div class="row">
      <div class="col-sm-6" v-for="movie in movies" v-bind:key="movie.id">
        <div class="card">
          <div class="card-body">
            <router-link v-bind:to="`movie/${movie.id}`">
              <h3>{{ movie.title }}</h3>
              <p></p>
            </router-link>
          </div>
        </div>
      </div>
    </div>
    <div></div>
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
