<template>
  <div class="input-container">
    <h1>{{ title }}</h1>
    <input type="text" v-on:keyup="$emit('inputChanges', $event.target.value)" />
  </div>
</template>

<script>
export default {
  props: ['title']
}
</script>

<style scoped>
  .input-container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: yellow;
    width: 100%;
    height: 110px;
    padding: 10px;
  }

  input{
    border-radius: 15px;
  }
</style>
