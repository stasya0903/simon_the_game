<template>
  <div class="game-options">
    <h2>Уровень Сложности:</h2>
    <input type="radio" name="mode" value="normal" checked>Легкий<br>
    <input type="radio" name="mode" value="sound-only">Sound Only<br>
    <input type="radio" name="mode" value="light-only">Light Only<br>
  </div>

</template>

<script>

export default {
  name: 'Options.vue',

};
</script>

<style scoped>

</style>
