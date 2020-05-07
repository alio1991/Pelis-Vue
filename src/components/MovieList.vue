<template>
  <div class="list">
      <movie-card @cardSelected="cardSelected" v-bind:isFavorite="isFavorite" v-for="(movie) in movies" :key="movie.Imdb" v-bind:movie=movie></movie-card>
  </div>
</template>

<script>
import MovieCard from './MovieCard.vue'


export default {
  props: {
    movies: Array,
    isFavorite: Boolean
  },
  components: {
    MovieCard
  },
  methods: {
    cardSelected(obj) {
      this.$emit('cardSelected', obj)
    },
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  :host{
    width: 100%;
    height: 100%;
  }

  .list{
    display: flex;
    flex-wrap: wrap;
  }
</style>
