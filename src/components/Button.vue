<template>
  <li :class="{'active':isActive}" @click="makeAction()">
    <Audio :num="num" :ref="refName"></Audio>
  </li>

</template>

<script>
import Audio from './Audio.vue';

export default {

  name: 'Button',
  components: { Audio },
  props: {
    num: Number,
  },

  data() {
    return {
      isActive: false,
      refName: `audio${this.num}`,
    };
  },
  methods: {
    makeAction() {
      this.makeSound();
      this.changeColor();
    },
    makeSound() {
      const el = this.$refs[this.refName].$el;
      el.play();
    },
    changeColor() {
      this.isActive = !this.isActive;
      setTimeout(() => this.isActive = !this.isActive, 500);
    },
  },
};
</script>

<style scoped>

</style>
