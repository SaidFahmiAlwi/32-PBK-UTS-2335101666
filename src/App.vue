<script setup>
import { ref } from 'vue'

// Data untuk menyimpan daftar kegiatan
const kegiatan = ref([ ])

// Data untuk menyimpan input dari user
const kegiatanBaru = ref('')

// Data untuk memilih filter
const filterSelesai = ref(null)  // null berarti menampilkan semua, false untuk belum selesai, true untuk selesai

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

// Fungsi untuk menyaring kegiatan berdasarkan status selesai
const filterKegiatan = () => {
  // Menampilkan semua jika filterSelesai bernilai null
  if (filterSelesai.value === null) {
    return kegiatan.value
  }
  return kegiatan.value.filter(item => item.selesai === filterSelesai.value)
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

    <!-- Filter untuk memilih hanya kegiatan yang belum selesai -->
    <div class="filter-container">
      <button @click="filterSelesai = false" :class="{ active: filterSelesai === false }" class="filter-btn">Belum Selesai</button>
      <button @click="filterSelesai = true" :class="{ active: filterSelesai === true }" class="filter-btn">Selesai</button>
      <button @click="filterSelesai = null" :class="{ active: filterSelesai === null }" class="filter-btn">Tampilkan Semua</button>
    </div>

    <!-- Daftar kegiatan -->
    <ul class="kegiatan-list">
      <li v-for="(item, index) in filterKegiatan()" :key="index" :class="{ selesai: item.selesai }">
        <input type="checkbox" :checked="item.selesai" @click="toggleSelesai(index)" class="checkbox" />
        <span :class="{ 'strikethrough': item.selesai }">{{ item.text }}</span>
        <button @click="hapusKegiatan(index)" class="btn hapus">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
/* Background image */
body {
  background-image: url('https://source.unsplash.com/random/1600x900'); /* Gambar latar belakang acak */
  background-size: cover;
  background-position: center;
  height: 100vh;
  margin: 0;
  font-family: 'Arial', sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  background-attachment: fixed;
}

/* Container untuk Todo List */
.todolist-container {
  margin: 0 auto;
  max-width: 600px;
  padding: 40px;
  background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent background agar konten tetap terbaca */
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  position: relative;
  z-index: 1;
  backdrop-filter: blur(10px); /* Efek blur untuk latar belakang */
}

/* Judul */
h2 {
  text-align: center;
  font-size: 2.5rem;
  color: #2c3e50;
  margin-bottom: 20px;
}

/* Input dan Button */
.input-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.input {
  padding: 0.8em;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  width: 60%;
  font-size: 1rem;
}

.btn {
  padding: 0.8em 1.5em;
  border-radius: 8px;
  color: white;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
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
  background-color: #ff4d4d;
  margin-left: 10px;
}

.hapus:hover {
  background-color: #e44d4d;
}

/* Filter Button */
.filter-container {
  text-align: center;
  margin-bottom: 30px;
}

.filter-btn {
  padding: 0.6em 1.2em;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  margin: 0 8px;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  background-color: #369870;
}

.filter-btn.active {
  background-color: #369870;
}

/* Daftar kegiatan */
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
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.kegiatan-list li:hover {
  background-color: #f7f7f7;
}

.kegiatan-list li.selesai {
  background-color: #e6f7e5; /* Hijau muda saat selesai */
}

.checkbox {
  margin-right: 15px;
  transform: scale(1.5);
  transition: all 0.3s ease;
}

.strikethrough {
  text-decoration: line-through;
  color: #888;
}

/* Responsif untuk perangkat kecil */
@media (max-width: 600px) {
  .input {
    width: 75%;
  }

  .btn {
    width: 100%;
  }

  .filter-btn {
    padding: 0.5em 1em;
  }
}
</style>
