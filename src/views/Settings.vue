<template>
  <div class="settings-page">
    <h2>Ayarlar</h2>
    <Settings @toggle-theme="toggleTheme" @clear-tasks="clearTasks" />
  </div>
</template>

<script>
import Settings from '../components/Settings.vue';

export default {
  components: { Settings },
  methods: {
    toggleTheme() {
      this.$emit('toggle-theme');
    },
    clearTasks() {
      this.$emit('clear-tasks');
    },
  },
};
</script>

<style>
.settings-page {
  padding: 20px;
}
</style>
