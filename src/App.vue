<template>
  <div>
    <form @submit.prevent="tambahData()">
      <table align="center" cellpadding="5">
        <tr>
          <td>Nama</td>
          <td>:</td>
          <td>
            <input type="text" v-model="inputData.nama" required />
          </td>
        </tr>
        <tr>
          <td>Kelas</td>
          <td>:</td>
          <td>
            <input type="text" v-model="inputData.kelas" required />
          </td>
        </tr>
        <tr>
          <td>Jurusan</td>
          <td>:</td>
          <td><input type="text" v-model="inputData.jurusan" required /></td>
        </tr>
        <tr>
          <td>
            <button type="submit">Kirim!</button>
          </td>
        </tr>
      </table>
    </form>
    <table align="center" border="1" cellspacing="0" cellpadding="5">
      <tr>
        <th>#</th>
        <th>Nama</th>
        <th>Kelas</th>
        <th>Jurusan</th>
        <th>Action</th>
      </tr>
      <tr v-for="(siswa, index) in daftarSiswa" v-bind:key="index">
        <th>
          {{ index + 1 }}
        </th>
        <td>{{ siswa.nama }}</td>
        <td>{{ siswa.kelas }}</td>
        <td>{{ siswa.jurusan }}</td>
        <td>
          <button type="button" @click="hapusData(index)">Hapus</button>
          |
          <button type="button" @click="editData(index)">Edit</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
  },
  data() {
    return {
      daftarSiswa: [
        {
          nama: "Muhammad Refdi",
          kelas: "XII",
          jurusan: "Rpl",
        },
        {
          nama: "Fachri Ardhana Dly",
          kelas: "XII",
          jurusan: "Rpl",
        },
        {
          nama: "Fikri Harahap",
          kelas: "XII",
          jurusan: "Rpl",
        },
      ],
      inputData: {
        nama: "",
        kelas: "",
        jurusan: "",
      },
      selectedId: "",
      method: "add",
    };
  },
  methods: {
    tambah() {
      this.nomor++;
    },
    tambahData() {
      if (this.method == "add") {
        this.daftarSiswa.push(this.inputData);
        this.inputData = {
          nama: "",
          kelas: "",
          jurusan: "",
        };
        this.method = "add";
      } else {
        this.daftarSiswa[this.selectedId].nama = this.inputData.nama;
        this.daftarSiswa[this.selectedId].kelas = this.inputData.kelas;
        this.daftarSiswa[this.selectedId].jurusan = this.inputData.jurusan;
        this.inputData = {
          nama: "",
          kelas: "",
          jurusan: "",
        };
        this.method = "add";
      }
    },
    hapusData(id) {
      this.daftarSiswa.splice(id, 1);
    },
    editData(id) {
      this.inputData = {
        nama: this.daftarSiswa[id].nama,
        kelas: this.daftarSiswa[id].kelas,
        jurusan: this.daftarSiswa[id].jurusan,
      };
      this.selectedId = id;
      this.method = "edit";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input {
  outline: none;
}

button {
  color: black;
  cursor: pointer;
}
</style>
