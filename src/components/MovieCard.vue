<template>
  <div class="card">
    <h1>{{movie ? movie.Title : ''}}</h1>
    <img :src= getPoster()>
  </div>
</template>

<script>
export default {
  props: ['movie'],
  created: function() {

  },
  methods: {
    getPoster (){
      return this.movie.Poster === 'N/A' ? './no-image.png' : this.movie.Poster;
    }
  }

}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
