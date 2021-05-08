<template>
  <div class="timer-wrapper">
    <div class="timer">{{ hours }}:{{ minutes }}:{{ seconds }}</div>
    <button class="reset" @click="this.resetTimer">Reset</button>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "Timer",
  data() {
    return { timer: 0, seconds: 0, minutes: 0, hours: 0 };
  },
  mounted() {
    this.startTimer();
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.seconds++;
        if (this.seconds === 60) {
          this.seconds = 0;
          this.minutes++;
          if (this.minutes === 60) {
            this.minutes = 0;
            this.hours++;
          }
        }
      }, 1000);
    },
    resetTimer() {
      clearTimeout(this.timer);
      this.seconds = 0;
      this.minutes = 0;
      this.hours = 0;
      this.startTimer();
      eventBus.$emit("reset-game"); // Ивент для ресета игры
    },
  },
};
</script>

<style scoped>
.timer-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15%;
  margin-top: 10px;
}
.timer {
  display: flex;
  font: bold 20px Tahoma;
  justify-content: center;
  align-items: center;
}
</style>
