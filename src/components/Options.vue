<template>
  <div class="game-options">
    <h2>Game Options:</h2>
    <input type="radio" name="mode" value="normal" checked>Normal<br>
    <input type="radio" name="mode" value="sound-only">Sound Only<br>
    <input type="radio" name="mode" value="light-only">Light Only<br>
    <input type="radio" name="mode" value="free-board">Free board
  </div>
</template>

<script>
export default {
  name: 'Options.vue',
};
</script>

<style scoped>

</style>
