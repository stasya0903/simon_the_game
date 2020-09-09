<template>
  <li :class="{'active':isActive}" @click="makeAction()"></li>
</template>

<script>
export default {
  name: 'Button',
  props: {
    num: Number,
  },
  data() {
    return {
      isActive: false;
    };
  },
  methods: {
    makeAction() {
      this.makeSound();
      this.changeColor();
      console.log('clicked');
    },
    makeSound() {

    },
    changeColor() {

    },
  },
};
</script>

<style scoped>

</style>
