<template>
  <div class="flex h-screen justify-center items-center flex-col">
    <div class="text-9xl">{{ formatTime }}</div>
    <div>
      <button
        class="bg-orange-300 rounded-lg mr-5 px-5 py-2"
        @click="startTimer"
        :disabled="timerActive"
      >
        Start
      </button>
      <button
        class="bg-orange-300 rounded-lg mr-5 px-5 py-2"
        @click="pauseTimer"
        :disabled="!timerActive"
      >
        Pause
      </button>
      <button
        class="bg-orange-300 rounded-lg px-5 py-2"
        @click="resetTimer"
        :disabled="!timerActive && time === initialTime"
      >
        Reset
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      initialTime: 25 * 60, // 25 minutes in seconds
      breakTime: 5 * 60, // 5 minutes in seconds
      time: 25 * 60,
      timerActive: false,
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.time / 60);
      const seconds = this.time % 60;
      return `${this.padTime(minutes)}:${this.padTime(seconds)}`;
    },
  },
  methods: {
    padTime(value) {
      return value < 10 ? `0${value}` : value;
    },
    startTimer() {
      this.timerActive = true;
      const timerInterval = setInterval(() => {
        if (this.time > 0 && this.timerActive) {
          this.time--;
        } else {
          this.timerActive = false;
          clearInterval(timerInterval);
          if (this.time === 0) {
            // If timer ran out, start the break
            this.time = this.breakTime;
            setTimeout(() => {
              // After the break, reset to 25 minutes
              this.time = this.initialTime;
            }, this.breakTime * 1000);
          }
        }
      }, 1000);
    },
    pauseTimer() {
      this.timerActive = false;
    },
    resetTimer() {
      this.time = this.initialTime;
      this.timerActive = false;
    },
  },
};
</script>

<style scoped>
/* Add your component styles here */
</style>
