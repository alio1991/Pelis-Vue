<template>
  <div id="app">
    <InputSearch @inputChanges="inputChanges"></InputSearch>
    <MovieList v-bind:movies="mutableList" />
  </div>
</template>

<script>
import MovieList from "./components/MovieList.vue";
import InputSearch from "./components/InputSearch.vue";

export default {
  name: "App",
  components: {
    MovieList,
    InputSearch
  },
  data: function() {
    return {
      inputValue: "Spiderman",
      page: 1,
      type: "movie",
      mutableList: []
    };
  },
  props: {
    movies: {
      type: Array
    }
  },
  created: function() {
    this.getMovies();
  },
  methods: {
    setMovies(movies) {
      this.movies = movies;
    },
    inputChanges(newInput) {
      this.inputValue = newInput;
      this.getMovies();
    },
    getMovies() {
      fetch(
        `https://www.omdbapi.com/?s=${this.inputValue}&plot=full&apikey=e477ed6a&page=${this.page}&type=${this.type}`
      )
        .then(response => {
          return response.json();
        })
        .then(result => {
          if (result.Search && result.Search.length > 0) {
            this.mutableList = result.Search;
          } else {
            this.mutableList = [];
          }
        })
        .catch(err => {
          console.log("Se ha producido un error: " + err);
        });
    }
  }
};
</script>

<style>
  :host {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin: 0;
    padding: 0;
  }
</style>
