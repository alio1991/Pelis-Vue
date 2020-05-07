<template>
  <div id="app">
    <InputSearch title="Buscador de películas" @inputChanges="inputChanges"></InputSearch>
    <div class="main">
      <MovieList class="favorites" @cardSelected="cardSelected" v-bind:isFavorite="true" v-bind:movies="favorites" />
      <MovieList class="standard" @cardSelected="cardSelected" v-bind:isFavorite="false" v-bind:movies="movies" />
    </div>
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
      movies: [],
      favorites: []
    };
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
    cardSelected(obj) {
      console.log(obj);
      if(obj.isFavorite){
        console.log('Favorita');
        
        this.favorites = [...this.favorites.filter(elem => elem.imdbID !== obj.card.imdbID)]
      }else{
        if(!this.favorites.includes(obj.card)){
          this.favorites.push(obj.card);
        }
      }
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
            this.movies = result.Search;
          } else {
            this.movies = [];
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
  }

  #app {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  .main{
    display: flex;
    width: 100%;
  }

  .favorites{
    width: 30%;
    height: 100%
  }

  .standard{
    width: 70%;
    height: 100%
  }

</style>
