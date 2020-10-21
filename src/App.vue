<template>
  <div>
    <div class="header-wrapper">
      <StartButton
        class="start-button"
        :start="start"
        @gameStarted="start = $event">
      </StartButton>
      <Timer
        :start="start">
      </Timer>
    </div>
    <Game
      :start="start">
    </Game>
  </div>
</template>

<script>
import StartButton from "./StartButton";
import Timer from "./Timer";
import Game from "./Game";


export default {
  name: 'app',
  components: {Game, Timer, StartButton},
  data () {
    return {
      start: false,
    }
  },
}
</script>

<style>
  .header-wrapper {
    display: flex;
    padding-top: 20px;
    padding-bottom: 20px;
    position: relative;
    min-height: 80px;
  }
</style>
