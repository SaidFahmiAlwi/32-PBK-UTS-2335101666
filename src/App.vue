<script setup>
import { ref } from 'vue'

// Data untuk menyimpan daftar kegiatan
const kegiatan = ref([
  'Belajar Vue 3',
  'Mengerjakan UTS',
  'Push project ke GitHub'
])

// Data untuk menyimpan input dari user
const kegiatanBaru = ref('')

// Fungsi untuk menambahkan kegiatan
const tambahKegiatan = () => {
  if (kegiatanBaru.value.trim() !== '') {
    kegiatan.value.push(kegiatanBaru.value)
    kegiatanBaru.value = ''
    console.log(kegiatan.value) // Menampilkan daftar kegiatan di konsol
  }
}
</script>

<template>
  <div>
    <h2>Daftar Kegiatan:</h2>

    <!-- Input untuk menambah kegiatan -->
    <input
      v-model="kegiatanBaru"
      type="text"
      placeholder="Masukkan kegiatan baru"
    />
    <button @click="tambahKegiatan">Tambah</button>

    <!-- Daftar kegiatan -->
    <ul>
      <li v-for="(item, index) in kegiatan" :key="index">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
input {
  padding: 0.5em;
  margin-right: 0.5em;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 0.5em 1em;
  background-color: #42b883;
  border: none;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #369870;
}
</style>
