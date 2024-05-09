<template>
  <div id="app">
    <h1 class="judul">APLIKASI INTERAKTIF</h1>

    <div class="input-wrapper">
      <input type="text" v-model="inputTeks" placeholder="Ketik teks di sini" class="input-teks" />
      <button @click="ubahTeks" class="btn-ubah">Tambah Teks</button>
    </div>

    <div class="output-wrapper">
      <h2>Riwayat ({{ riwayat.length }} dari {{ batasRiwayat }})</h2>
      <div class="input-jumlah">
        <label for="jumlah">Jumlah:</label>
        <input type="number" id="jumlah" v-model="batasRiwayat" min="1" :max="riwayat.length" />
      </div>
      <ul class="riwayat-list">
        <li v-for="(item, index) in riwayat.slice(0, batasRiwayat)" :key="index" :class="{ 'coret': item.checked }">
          <input type="checkbox" v-model="item.checked" class="checkbox" />
          {{ item.teks }}
          <button @click="hapusTeks(index)" class="btn-hapus">Hapus</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputTeks: "",
      riwayat: [],
      batasRiwayat: 10, // batas jumlah riwayat
    };
  },
  methods: {
    ubahTeks() {
      if (this.riwayat.length >= this.batasRiwayat) {
        this.riwayat.shift(); // hapus item pertama jika sudah mencapai batas
      }
      this.riwayat.push({ teks: this.inputTeks, checked: false });
      this.inputTeks = "";
    },
    hapusTeks(index) {
      this.riwayat.splice(index, 1);
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
  margin-top: 50px;
}

.judul {
  color: #9ac5e5;
}

.input-wrapper {
  margin-bottom: 20px;
}

.input-teks {
  padding: 10px;
  border-radius: 5px;
  font-size: 16px;
  width: 200px;
  margin-right: 10px;
}

.btn-ubah {
  background-color: #4fb19d;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.output-wrapper {
  background-color: #e5c6c3;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.output {
  font-size: 18px;
  color: #333;
}

.riwayat-list {
  padding: 0;
  margin: 25;
  padding: 20px;
  font-size: 20px;
}

.btn-hapus {
  background-color: #ff4d4d;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 12px;
  margin-left: 10px;
}

.checkbox {
  margin-right: 10px;
}

.coret {
  text-decoration: line-through;
}

.input-jumlah {
  margin-bottom: 10px;
}
</style>
