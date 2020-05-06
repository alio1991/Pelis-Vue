<template>
  <div class="input-container">
    <input type="text" v-on:keyup="$emit('inputChanges', $event.target.value)" />
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
  .input-container{
    background-color: yellow;
    height: 110px;
  }
</style>
