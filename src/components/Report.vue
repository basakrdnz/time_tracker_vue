<template>
  <div class="report">
    <h3>Toplam Çalışma Süresi: {{ formatTime(totalTime) }}</h3>
  </div>
</template>

<script>
export default {
  props: ['totalTime'],
  methods: {
    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = seconds % 60;
      return `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`;
    },
  },
};
</script>

<style>
.report {
  margin-top: 20px;
  font-size: 1.2em;
  font-weight: bold;
  text-align: center;
}
</style>
