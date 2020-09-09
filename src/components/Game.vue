<template>
  <div class="wrapper">
    <div class="game-board">
      <div class="simon">
        <ul>
          <Button @userStep="addStep(1)" class="tile red" ref='1' :num="1"></Button>
          <Button @userStep="addStep(2)" class="tile blue" ref='2' :num="2" ></Button>
          <Button @userStep="addStep(3)" class="tile yellow" ref='3' :num="3" ></Button>
          <Button @userStep="addStep(4)" class="tile green" ref='4' :num="4" ></Button>
        </ul>
      </div>
    </div>
    <Info @start="start" :round="this.round" :msg="this.msg"></Info>
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
      userPlaying: false,
      userAnswer: [],
      msg: 'Нажмите старт для начала',
    };
  },
  methods: {
    start() {
      this.playRound();
    },
    playRound() {
      this.msg = 'Смотрите';
      this.showSequence();
      this.msg = 'Повторите';
      this.userPlaying = true;
    },
    showSequence() {
      this.clearSequence();
      this.generateSequence();
      this.clickButtons();
    },
    addStep(number) {
      this.userAnswer = [...this.userAnswer, number];
      this.isThisStepCorrect(number) ? this.continueGame() : this.gameOver();
    },

    isThisStepCorrect(number) {
      const expectedAnswer = this.sequence[this.userAnswer.length - 1];
      return (expectedAnswer === +number);
    },
    continueGame() {
      if (this.userAnswer.length === this.sequence.length) {
        this.nextRound();
      }
    },
    nextRound() {
      this.userAnswer = [];
      this.round++;
      this.playRound();
    },
    gameOver() {
      this.msg = 'Вы проиграли, нажмите старт для начала';
    },
    clearSequence() {
      this.sequence = [];
    },
    generateSequence() {
      for (let i = 0; i < this.round; i++) {
        const randomNumber = Math.floor((Math.random() * 4) + 1);
        this.sequence = [...this.sequence, randomNumber];
      }
    },
    clickButtons() {
      for (let i = 0; i < this.sequence.length; i++) {
        setTimeout(() => {
          this.$refs[this.sequence[i]].action();
        }, 1500 * (i + 1));
      }
    },
  },
};
</script>

<style scoped>

</style>
