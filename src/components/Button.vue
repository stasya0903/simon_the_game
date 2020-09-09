<template>
  <li :id='num' :class="{'active':isActive}" @action="action()" @click="(event)=>makeAction(event)">
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
    userPlaying: Boolean,
  },

  data() {
    return {
      isActive: false,
      refName: `audio${this.num}`,
    };
  },
  methods: {
    action(){
      this.makeSound();
      this.changeColor();
    },
    makeAction(event) {
      this.action();
      this.$emit('userStep');
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
