<template>
  <div class="movies-show">
    <div class="container">
      <h2>{{ movie.title }}</h2>
      <h3>{{ movie.year }}</h3>
      <h3>{{ movie.plot }}</h3>
    </div>
    <router-link v-bind:to="`/movie/${movie.id}/edit`">See more info</router-link>
    <br />
    <br />
    <button v-on:click="destroyMovie(movie)">Destroy Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    this.showMovie();
  },
  methods: {
    showMovie: function () {
      axios.get("/api/movie/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.movie = response.data;
      });
    },
    destroyMovie: function (movie) {
      axios.delete("/api/movie/" + movie.id).then(() => {
        console.log("Movie destroyed");
        this.$router.push("/movie");
      });
    },
  },
};
</script>
