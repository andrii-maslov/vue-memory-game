<template>
  <button
    class="start-button"
    @click="startGame">
    Start game
  </button>
</template>

<script>
export default {
  name: "StartButton",
  data() {
    return {

    }
  },
  props: {
    start: Boolean,
  },
  methods: {
    startGame() {
      this.$emit('gameStarted', true);
    },
  }
}
</script>

<style scoped>
.start-button {
  padding: 10px;
  margin-right: 50px;
  height: fit-content;
}
</style>
