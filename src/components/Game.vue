<template>
  <div class="wrapper">
    <div class="game-board">
      <div class="simon">
        <ul>
          <Button class="tile red" ref='1' :num="1"></Button>
          <Button class="tile blue" ref='2' :num="2"></Button>
          <Button class="tile yellow" ref='3' :num="3"></Button>
          <Button class="tile green" ref='4' :num="1"></Button>
        </ul>
      </div>
    </div>
    <Info @start="start" :round="this.round"></Info>
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
      round: 1,
    };
  },
  methods: {
    clearSequence() {
      this.sequence = [];
    },
    generateSequence() {
      // eslint-disable-next-line no-plusplus
      for (let i = 0; i < this.round; i++) {
        const randomNumber = Math.floor((Math.random() * 4) + 1);
        this.sequence = [...this.sequence, randomNumber];
      }
    },
    start() {
      this.playRound();
    },

    playRound() {
      this.clearSequence();
      this.generateSequence();
      this.clickButtons();
      // eslint-disable-next-line no-plusplus
      this.round++;
    },
    clickButtons() {
      for (let i = 0; i < this.sequence.length; i++) {
        setTimeout(() => {
          this.$refs[this.sequence[i]].$el.click();
        }, 500 * (i + 1));
      }
    },
  },
};
</script>

<style scoped>

</style>
