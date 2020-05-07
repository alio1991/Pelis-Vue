<template>
  <div class="card" v-bind:class="{ favorite: isFavorite }" v-on:click="$emit('cardSelected', {card: movie, isFavorite:isFavorite})">
    <p>{{movie ? movie.Title : ''}}</p>
    <img :src= getPoster()>
  </div>
</template>

<script>
export default {
  props: ['movie','isFavorite'],
  methods: {
    getPoster (){
      return this.movie.Poster === 'N/A' ? './no-image.png' : this.movie.Poster;
    }
  }

}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .card{
    cursor: pointer;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 250px;
    height: 400px;
    background-color: lightblue;
    margin: 5px;
    padding: 5px;
    box-sizing: border-box;
    border-radius: 15px;
    border: solid 1px black;
  }

  .favorite{
    cursor: pointer;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 100px;
    height: 190px;
    background-color: lightcoral;
    margin: 5px;
    padding: 5px;
    box-sizing: border-box;
    border-radius: 15px;
    border: solid 1px black;
    font-size: 10px;
  }

  .card img{
    height: 300px;
    width: 200px;
    border-bottom-left-radius: 15px;
    border-bottom-right-radius: 15px;
  }

  .favorite img{
    height: 110px;
    width: 90px;
    border-bottom-left-radius: 15px;
    border-bottom-right-radius: 15px;
  }
</style>
