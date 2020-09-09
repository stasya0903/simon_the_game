<template>
  <audio  controls class="audio" preload="auto">
    <source :src="OggSrs" type="audio/ogg">
    <source :src="Mp3Src" type="audio/mpeg">
  </audio>
</template>

<script>
export default {
  name: 'Audio.vue',
  props: {
    num: Number,
  },
  data() {
    return {
      OggSrs: require(`../assets/sounds/${this.num}.ogg`),
      Mp3Src: require(`../assets/sounds/${this.num}.mp3`),
    };
  },
};
</script>

<style scoped>
.audio{

}
</style>
