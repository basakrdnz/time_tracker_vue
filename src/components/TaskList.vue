<template>
  <div class="task-list">
    <h2>Görevler</h2>
    <div v-for="task in tasks" :key="task.id" class="task-item">
      <h3>{{ task.name }}</h3>
      <p>{{ task.description }}</p>
      <p>Kategori: {{ task.category }}</p>
      <div class="time-display" :class="{ active: task.isRunning }">
        {{ formatTime(task.timeSpent) }}
      </div>
      <p v-if="task.isCompleted" class="completed-message">
        Tamamlandı - Toplam Süre: {{ formatTime(task.timeSpent) }}
      </p>
      <button :class="{ 'start-button': !task.isRunning && !task.isCompleted, 'stop-button': task.isRunning }" @click="toggleTimer(task)" v-if="!task.isCompleted">
        {{ task.isRunning ? 'Durdur' : 'Başlat' }}
      </button>
      <button @click="completeTask(task)" class="complete-button" v-if="!task.isCompleted">Bitir</button>
      <button @click="resetTaskTimer(task)" class="reset-button" v-if="!task.isCompleted">Sıfırla</button>
      <button @click="deleteTask(task.id)" class="delete-button">Sil</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['tasks'],
  methods: {
    toggleTimer(task) {
      if (!task.isRunning) {
        this.startTimer(task);
      } else {
        this.stopTimer(task);
      }
    },
    startTimer(task) {
      task.isRunning = true;
      task.intervalId = setInterval(() => {
        task.timeSpent++;
      }, 1000);
    },
    stopTimer(task) {
      clearInterval(task.intervalId);
      task.intervalId = null;
      task.isRunning = false;
    },
    resetTaskTimer(task) {
      this.stopTimer(task);
      task.timeSpent = 0;
    },
    completeTask(task) {
      this.stopTimer(task);
      task.isCompleted = true;
      task.completedAt = new Date().toLocaleString();
    },
    deleteTask(id) {
      this.$emit('delete-task', id);
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
.task-list {
  max-width: 800px; /* Liste genişliği sınırlandı */
  margin: 20px auto; /* Ortalandı */
  text-align: center; /* Başlıklar ve içerik ortalandı */
}

.task-list h2 {
  color: #8338EC; /* Mor başlık */
  font-size: 1.8em;
  margin-bottom: 20px;
}

/* Görev Kutuları */
.task-item {
  background-color: rgba(131, 56, 236, 0.1); /* Hafif saydam mor arka plan */
  border: 2px solid #8338EC; /* Mor kenarlık */
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Hafif gölge */
  transition: transform 0.3s, box-shadow 0.3s;
}

/* Hover ile büyüme ve gölge */
.task-item:hover {
  transform: scale(1.02);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

/* Zaman Görünümü */
.time-display {
  font-size: 1.2em;
  font-weight: bold;
  padding: 10px;
  margin: 15px auto;
  color: #333;
  background-color: rgba(255, 190, 11, 0.1); /* Saydam sarı arka plan */
  border: 2px solid #FFBE0B; /* Sarı kenarlık */
  border-radius: 8px;
  width: 150px;
}

.time-display.active {
  color: white;
  background-color: #3A86FF; /* Mavi arka plan */
}

/* Tamamlandı Mesajı */
.completed-message {
  color: #FF006E; /* Pembe */
  font-weight: bold;
  margin-top: 10px;
}

/* Butonlar */
button {
  margin: 5px;
  padding: 10px 15px;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

button:hover {
  transform: scale(1.05); /* Hafif büyüme */
}

/* Başlat Butonu */
.start-button {
  background-color: #4CAF50;
}

.stop-button {
  background-color: #FB5607; /* Turuncu */
}

.complete-button {
  background-color: #FFBE0B; /* Sarı */
}

.reset-button {
  background-color: #8338EC; /* Mor */
}

.delete-button {
  background-color: #FF006E; /* Pembe */
}
</style>
