<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">The Movie App</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div id="nav">
          <router-link to="/">Home</router-link>
          |
          <router-link to="/about">About</router-link>
          |
          <span v-if="!isLoggedIn()">
            <router-link to="/signup">Sign up</router-link>
          </span>
          |
          <span v-if="!isLoggedIn()">
            <router-link to="/login">Log in</router-link>
          </span>
          |
          <router-link to="/logout">Logout</router-link>
          |
          <router-link to="/movie">Movie List</router-link>
          |
          <router-link to="/movies-new">Create a new movie entry</router-link>
        </div>
      </div>
    </nav>

    <router-view />
  </div>
</template>

<style>
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  background-image: url("./assets/bush.png");
}
</style>

<script>
export default {
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
