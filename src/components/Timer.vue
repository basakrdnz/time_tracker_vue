<template>
  <div class="timer">
    <p>{{ formatTime(task.timeSpent) }}</p>
    <button @click="toggleTimer">{{ isRunning ? 'Durdur' : 'Başlat' }}</button>
  </div>
</template>

<script>
export default {
  props: ['task'],
  data() {
    return { isRunning: false, intervalId: null };
  },
  methods: {
    toggleTimer() {
      this.isRunning ? this.stopTimer() : this.startTimer();
    },
    startTimer() {
      this.isRunning = true;
      this.intervalId = setInterval(() => {
        this.task.timeSpent++;
        this.$emit('update-time', this.task.id, this.task.timeSpent);
      }, 1000);
    },
    stopTimer() {
      clearInterval(this.intervalId);
      this.intervalId = null;
      this.isRunning = false;
    },
    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = seconds % 60;
      return `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`;
    },
  },
};
</script>

<style>
.timer {
  margin-top: 10px;
}
</style>
