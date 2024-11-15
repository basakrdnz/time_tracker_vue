<template>
  <div class="task-form">
    <h2>Yeni Görev Ekle</h2>
    <form @submit.prevent="addTask">
      <input type="text" v-model="taskName" placeholder="Görev adı" required />
      <textarea v-model="taskDescription" placeholder="Görev açıklaması"></textarea>
      <select v-model="taskCategory">
        <option value="">Kategori Seç</option>
        <option value="Code">Code</option>
        <option value="Personal">Personal</option>
        <option value="Gym">Gym</option>
      </select>
      <button type="submit">Ekle</button>
    </form>

    <!-- Popup Mesaj -->
    <div v-if="showPopup" class="popup">
      Görev başarıyla eklendi!
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskName: '',
      taskDescription: '',
      taskCategory: '',
      showPopup: false, // Popup kontrolü için durum
    };
  },
  methods: {
    addTask() {
      this.$emit('task-added', {
        name: this.taskName,
        description: this.taskDescription,
        category: this.taskCategory,
        timeSpent: 0,
        isCompleted: false,
      });
      this.taskName = '';
      this.taskDescription = '';
      this.taskCategory = '';

      // Popup mesajını göster
      this.showPopup = true;

      // 3 saniye sonra popup mesajını gizle
      setTimeout(() => {
        this.showPopup = false;
      }, 3000);
    },
  },
};
</script>

<style>
/* Form Konteyner */
.task-form {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  background-color: rgba(131, 56, 236, 0.1); /* Hafif saydam mor arka plan */
  border: 2px solid #8338EC;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Hafif gölge */
  text-align: center;
}

/* Başlık */
.task-form h2 {
  color: #8338EC;
  font-size: 1.8em;
  margin-bottom: 20px;
}

/* Input, Textarea ve Select */
input, textarea, select {
  display: block;
  width: 90%;
  margin: 10px auto;
  padding: 10px;
  background-color: rgba(255, 255, 255, 0.7);
  border: 1px solid #3A86FF;
  border-radius: 5px;
  font-size: 1em;
  color: #333;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1); /* İç gölge */
  transition: box-shadow 0.3s, transform 0.2s;
}

input:hover, textarea:hover, select:hover,
input:focus, textarea:focus, select:focus {
  box-shadow: 0 0 8px #3A86FF; /* Mavi parıltı */
  transform: scale(1.02);
  outline: none;
}

/* Buton */
button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #FB5607; /* Turuncu */
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

button:hover {
  background-color: #FF006E; /* Pembe */
  transform: scale(1.05);
}

/* Popup Mesaj Stili */
.popup {
  margin-top: 20px;
  padding: 10px 15px;
  background-color: #4caf50; /* Yeşil arka plan */
  color: white;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  animation: fadein 0.5s, fadeout 0.5s 2.5s; /* Mesajın yavaşça gelmesi ve kaybolması */
}

/* Fade Animasyonları */
@keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fadeout {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
</style>
