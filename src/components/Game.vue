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
    <Info @start="start"></Info>
    <Options></Options>
  </div>
</template>

<script>

import Button from './Button.vue';
import Info from './Info.vue';
import Options from './Options.vue';

export default {
  name: 'Game',
  components: {
    Button,
    Info,
    Options,
  },
  data() {
    return {
      sequence: [],
    };
  },
  methods: {
    generateSequence() {
      for (let i = 0; i < 4; i++) {
        const randomNumber = Math.floor((Math.random() * 4) + 1);
        this.sequence = [...this.sequence, randomNumber];
      }
    },
    start() {
      this.generateSequence();
    },
    clickButtons() {
      for(i=0, i<this.sequence.length, i++)
      this.$ref[i].click();
    },
  },
};
</script>

<style scoped>

</style>
