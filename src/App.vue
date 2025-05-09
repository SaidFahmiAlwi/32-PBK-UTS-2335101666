<script setup>
import { ref } from 'vue'

// Data untuk menyimpan daftar kegiatan
const kegiatan = ref([ ])

// Data untuk menyimpan input dari user
const kegiatanBaru = ref('')

// Fungsi untuk menambahkan kegiatan
const tambahKegiatan = () => {
  if (kegiatanBaru.value.trim() !== '') {
    kegiatan.value.push({ text: kegiatanBaru.value, selesai: false })
    kegiatanBaru.value = ''
    console.log(kegiatan.value) // Menampilkan daftar kegiatan di konsol
  }
}

// Fungsi untuk menghapus kegiatan berdasarkan index
const hapusKegiatan = (index) => {
  kegiatan.value.splice(index, 1)
  console.log(kegiatan.value) // Menampilkan daftar kegiatan setelah dihapus
}

// Fungsi untuk menandai kegiatan selesai
const toggleSelesai = (index) => {
  kegiatan.value[index].selesai = !kegiatan.value[index].selesai
  console.log(kegiatan.value) // Menampilkan daftar kegiatan yang diperbarui
}
</script>

<template>
  <div class="todolist-container">
    <h2>Daftar Kegiatan:</h2>

    <!-- Input untuk menambah kegiatan -->
    <div class="input-container">
      <input
        v-model="kegiatanBaru"
        type="text"
        placeholder="Masukkan kegiatan baru"
        class="input"
      />
      <button @click="tambahKegiatan" class="btn tambah">Tambah</button>
    </div>

    <!-- Daftar kegiatan -->
    <ul class="kegiatan-list">
      <li v-for="(item, index) in kegiatan" :key="index" :class="{ selesai: item.selesai }">
        <input type="checkbox" :checked="item.selesai" @click="toggleSelesai(index)" class="checkbox" />
        <span :class="{ 'strikethrough': item.selesai }">{{ item.text }}</span>
        <button @click="hapusKegiatan(index)" class="btn hapus">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.todolist-container {
  font-family: 'Arial', sans-serif;
  margin: 0 auto;
  max-width: 600px;
  padding: 20px;
  background-color: #f4f7fb;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #333;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
  justify-content: center;
}

.input {
  padding: 0.5em;
  margin-right: 0.5em;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 60%;
}

.btn {
  padding: 0.5em 1em;
  border-radius: 5px;
  color: white;
  border: none;
  cursor: pointer;
}

.btn:hover {
  opacity: 0.8;
}

.tambah {
  background-color: #42b883;
}

.tambah:hover {
  background-color: #369870;
}

.hapus {
  background-color: red;
  margin-left: 10px;
}

.hapus:hover {
  background-color: #ff4d4d;
}

.kegiatan-list {
  list-style-type: none;
  padding: 0;
}

.kegiatan-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #ffffff;
  margin: 10px 0;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.kegiatan-list li.selesai {
  background-color: #e6f7e5; /* Tampilkan dengan latar belakang hijau muda ketika selesai */
}

.checkbox {
  margin-right: 10px;
  transform: scale(1.2);
}

.strikethrough {
  text-decoration: line-through;
  color: #888;
}

@media (max-width: 600px) {
  .input {
    width: 80%;
  }

  .btn {
    width: 100%;
  }
}
</style>
