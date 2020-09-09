<template>
  <div class="wrapper">
    <div class="game-board">
      <div class="simon">
        <ul>
          <Button @userStep="addStep(1)"
                  class="tile red"
                  ref='1'
                  :num="1"
                  :userPlaying="userPlaying"></Button>
          <Button @userStep="addStep(2)"
                  class="tile blue"
                  ref='2'
                  :num="2"
                  :userPlaying="userPlaying"></Button>
          <Button @userStep="addStep(3)"
                  class="tile yellow"
                  ref='3'
                  :num="3"
                  :userPlaying="userPlaying"></Button>
          <Button @userStep="addStep(4)"
                  class="tile green"
                  ref='4'
                  :num="4"
                  :userPlaying="userPlaying"></Button>
        </ul>
      </div>
    </div>
    <Info
      @start="start"
      :round="this.round"
      :msg="this.msg"
    ></Info>
    <Options
      @setLevel='setLevel'
      :levels="this.levels"
      :currentLevel="this.currentLevel"></Options>
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
      levels: [
        {
          value: 'light',
          speed: 1500,
          name: 'Легкий',
        },
        {
          value: 'middle',
          speed: 1000,
          name: 'Средний',
        },
        {
          value: 'hard',
          speed: 400,
          name: 'Сложный',

        },
      ],
      currentLevel: 'light',
      sequence: [],
      round: 1,
      userPlaying: false,
      userAnswer: [],
      msg: 'Нажмите старт для начала',
    };
  },
  computed: {
    speed() {
      return this.levels.find((el) => el.value === this.currentLevel).speed;
    },
  },
  methods: {
    start() {
      this.playRound();
    },
    playRound() {
      setTimeout(() => {
        this.msg = 'Смотрите';
        this.showSequence();
      }, 1000);
    },
    async showSequence() {
      await this.playSequence();
      setTimeout(() => {
        this.userPlaying = true;
        this.msg = 'Повторите';
      }, 1000);
    },

    playSequence() {
      this.clearSequence();
      this.generateSequence();
      return this.sequence.reduce(async (prev, nextId) => {
        await prev;
        return this.clickButton(nextId);
      }, Promise.resolve());
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
        this.userPlaying = false;
        setTimeout(() => {
          this.msg = 'Отлично!';
        }, 500);
      }
    },
    nextRound() {
      this.userAnswer = [];
      this.round++;
      this.playRound();
    },
    gameOver() {
      this.resetGame();
      this.msg = 'Вы проиграли, нажмите старт для начала';
    },
    resetGame() {
      this.sequence = [];
      this.round = 1;
      this.userPlaying = false;
      this.userAnswer = [];
      this.msg = 'Нажмите старт для начала';
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

    clickButton(number) {
      return new Promise((resolve) => {
        setTimeout(() => {
          this.$refs[number].action();
          resolve();
        }, this.speed);
      });
    },
    setLevel(level) {
      this.resetGame();
      this.currentLevel = level;
    },

  },
};
</script>

<style scoped>

</style>
