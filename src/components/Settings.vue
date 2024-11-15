<template>
  <div class="settings">
    <h2>Ayarlar</h2>
    <button @click="$emit('toggle-theme')">Tema Değiştir</button>
    <button @click="$emit('clear-tasks')">Tüm Görevleri Temizle</button>
  </div>
</template>

<style>
/* Konteyner */
.settings {
  margin: 20px auto;
  text-align: center;
  max-width: 400px; /* Genişlik sınırlandı ve ortalandı */
  padding: 20px;
  background-color: rgba(131, 56, 236, 0.1); /* Hafif saydam mor arka plan */
  border: 2px solid #8338EC; /* Mor kenarlık */
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Hafif gölge */
}

/* Başlık */
.settings h2 {
  color: #8338EC; /* Mor renk */
  font-size: 1.6em;
  margin-bottom: 20px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 2px;
}

/* Butonlar */
button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #3A86FF; /* Mavi */
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Hafif gölge */
  transition: background-color 0.3s, transform 0.2s, box-shadow 0.3s;
}

button:hover {
  background-color: #8338EC; /* Mor */
  transform: scale(1.05); /* Hafif büyüme */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); /* Daha belirgin gölge */
}

/* Butonlar Aktif Hale Gelirken */
button:active {
  transform: scale(0.95); /* Hafif küçülme */
}
</style>
