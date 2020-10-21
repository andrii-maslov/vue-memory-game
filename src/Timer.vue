<template>
  <div class="timer-wrapper">
    <p class="timer">
      {{ timeNumberToString() }}
    </p>
  </div>
</template>

<script>


export default {
  name: "Timer",
  props: {
    start: Boolean,
  },
  data() {
    return {
      timer: 0,
      interval: '',
    }
  },
  methods: {
    startTimer() {
      if (this.start) {
        this.interval = setInterval(this.timerCounter, 1000);
        return this.interval;
      }
    },
    timerCounter() {
      this.timer++;
    },
    timeNumberToString() {
      let seconds = this.timer % 60;
      seconds = seconds < 10 ? `0${seconds}` : seconds;

      let minutes = Math.floor(this.timer / 60);
      minutes = minutes < 10 ? `0${minutes}` : minutes;

      let hours = Math.floor(minutes / 60 / 60);

      return `${hours}:${minutes}:${seconds}`;
    }
  },
  watch: {
    start() {
      this.startTimer();
    }
  }
}

</script>

<style scoped>
  .timer-wrapper {
    position: absolute;
    left: 200px;
  }

  .timer {
    font-size: 20px;
  }
</style>
