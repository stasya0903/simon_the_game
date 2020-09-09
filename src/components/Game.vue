<template>
  <div class="wrapper">
    <div class="game-board">
      <div class="simon">
        <ul>
          <Button class="tile red" :num="1"></Button>
          <Button class="tile blue" :num="2"></Button>
          <Button class="tile yellow" :num="3"></Button>
          <Button class="tile green" :num="4"></Button>
        </ul>
      </div>

    </div>
      <Info></Info>
    <Options></Options>
    <div class="game-options"></div>
  </div>
</template>

<script>

import Button from './Button.vue';
import Info from './Info.vue';
import Options from './Options.vue';

export default {
  name: 'Game',
  components: {
    Button, Info, Options,
  },
};
</script>

<style scoped>

</style>
