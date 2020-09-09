<template>
  <div class="game-options">
    <h2>Уровень Сложности:</h2>
    <div v-for="item of this.levels" :key="item.index">
      <input type="radio"
             :checked="item.value === currentLevel"
             name="mode"
             :value="item.value"
             @input="$emit('setLevel', item.value)">{{item.name}}
              <br>
    </div>

  </div>

</template>

<script>

export default {
  name: 'Options.vue',
  props: {
    levels: Array,
    currentLevel: String,
  },

};
</script>

<style scoped>

</style>
