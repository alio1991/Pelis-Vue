<template>
  <div class="list">
    <movie-card v-for="(movie) in movies" :key="movie.Imdb" v-bind:movie=movie></movie-card>
  </div>
</template>

<script>
import MovieCard from './MovieCard.vue'


export default {
  props: {
    movies: Array
  },
  components: {
    MovieCard
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
