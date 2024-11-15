<template>
  <section :class="{ dark: isDarkMode }">
    <header>
      <h1>Time Tracker By Basak</h1>
    </header>

    <hr class="divider" />

    <main>
      <TaskForm @task-added="addTask" />
      <hr class="divider" />
      <TaskList
          :tasks="tasks"
          @start-timer="startTimer"
          @stop-timer="stopTimer"
          @delete-task="deleteTask"
      />
      <hr class="divider" />
    </main>

    <Report :totalTime="totalTime" />
    <hr class="divider" />
    <Settings @toggle-theme="toggleTheme" @clear-tasks="clearTasks" />
  </section>
</template>

<script>
import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';
import Report from './components/Report.vue';
import Settings from './components/Settings.vue';

export default {
  components: { TaskForm, TaskList, Report, Settings },
  data() {
    return {
      isDarkMode: false,
      tasks: [],
    };
  },
  computed: {
    totalTime() {
      return this.tasks.reduce((sum, task) => sum + (task.timeSpent || 0), 0);
    },
  },
  methods: {
    addTask(task) {
      this.tasks.push({ ...task, id: Date.now(), timeSpent: 0 });
    },
    startTimer(task) {
      task.startTime = Date.now();
    },
    stopTimer(task) {
      if (task.startTime) {
        const elapsed = Math.round((Date.now() - task.startTime) / 1000); // Saniye cinsinden
        task.timeSpent += elapsed;
        task.startTime = null;
      }
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    toggleTheme() {
      this.isDarkMode = !this.isDarkMode;
    },
    clearTasks() {
      this.tasks = [];
    },
  },
};
</script>

<style>
/* Karanlık Mod */
.dark {
  background-color: #121212;
  color: white;
}

/* Header */
header {
  text-align: center;
  padding: 20px;
  background-color: #893d88;
  color: white;
  font-size: 2.5em;
  color: #8338EC; /* Mor renk */
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
  background: linear-gradient(90deg, #FFBE0B, #FB5607, #FF006E, #8338EC, #3A86FF);
  -webkit-background-clip: text;
  color: transparent;
  animation: gradientMove 3s infinite;
}

/* Arka planda hareket eden bir renk geçişi efekti */
@keyframes gradientMove {
  0% {
    background-position: 0%;
  }
  100% {
    background-position: 100%;
  }
}

/* Divider (Şerit) */
.divider {
  border: none;
  height: 2px;
  background: linear-gradient(90deg, #FFBE0B, #FB5607, #FF006E, #8338EC, #3A86FF); /* Renk geçişi */
  margin: 20px 0; /* Alanlar arasındaki boşluk */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Hafif gölge */
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
