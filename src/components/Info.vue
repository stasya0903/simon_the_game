<template>
  <div class="game-info">
    <h2>Round: <span data-round="0">0</span></h2>
    <button data-action="start" >Start</button>
    <p data-action="lose">Sorry, you lost after <span data-round="0"></span> rounds!</p>
  </div>
</template>

<script>
export default {
  name: 'Info',
};
</script>

<style scoped>

</style>
