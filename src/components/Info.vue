<template>
  <div class="game-info">
    <h2>Round: {{round}}</h2>
    <button @click="$emit('start')" >Start</button>
    <p>{{msg}}</p>
  </div>
</template>

<script>
export default {
  name: 'Info',
  props: {
    round: Number,
    msg: String,
  },
};
</script>

<style scoped>

</style>
