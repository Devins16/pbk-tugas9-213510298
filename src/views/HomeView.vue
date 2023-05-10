<template>
<div>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" width="100" height="100">
  </div>

  <div>
     
     <h1>Remind Me!!</h1>
     <br>
     
    <label>Tampilkan kegiatan yang belum selesai</label>
    <input type="checkbox" v-model="showUncompleted">
      <ul>
      <li v-for="kegiatan in filterKegiatan" :key="kegiatan.id" :class="{ 'selesai': kegiatan.selesai }">
        <input type="checkbox" v-model="kegiatan.selesai" @change="checklistKegiatan(kegiatan)" />
        <span>{{ kegiatan.nama }}</span>
        <button @click="hapusKegiatan(kegiatan.id)">Hapus</button>
      </li>
    </ul>
      <ul>
          <li v-for="kegiatan in daftarKegiatan">
              <input type="checkbox" v-model="kegiatan.selesai">
              <span :class="{ selesai: kegiatan.selesai }">{{ kegiatan.nama }}</span>
              <button @click="hapusKegiatan(kegiatan)">Hapus</button>
          </li>
      </ul>
      <br>
      <br>
      <form @submit.prevent="tambahKegiatan">
          <input type="text" v-model="kegiatanBaru" placeholder="Tambah kegiatan anda..."> 
          <br>
          <button type="submit">Tambah</button>
      </form>
  </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            daftarKegiatan: [
                { nama: 'Bersihkan Kamar', selesai: false },
                { nama: 'Mandi', selesai: false },
                { nama: 'Buat Sarapan', selesai: false }
            ],
            kegiatanBaru: '',
            showUncompleted: false,
            
        }
    },
     computed: {
  filteredKegiatan() {
    if (this.showUncompleted) {
      return this.daftarKegiatan.filter((kegiatan) => !kegiatan.selesai)
    } else {
      return this.daftarKegiatan
    }
  },
},
    methods: {
        tambahKegiatan() {
            if (this.kegiatanBaru.trim() !== '') {
                this.daftarKegiatan.push({
                    nama: this.kegiatanBaru.trim(),
                    selesai: false
                })
                this.kegiatanBaru = ''
            }
        },
        hapusKegiatan(kegiatan) {
            const index = this.daftarKegiatan.indexOf(kegiatan)
            if (index > -1) {
                this.daftarKegiatan.splice(index, 1)
            }
        },
        checklistKegiatan(kegiatan) {
          kegiatan.selesai = !kegiatan.selesai
        }
    }
}
</script>

<style>

* {
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
 ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  
  li {
    display: flex;
    align-items: center;
    margin-bottom: 0.5rem;
    padding: 0.5rem;
    background-color: #f5f5f5;
    border-radius: 0.25rem;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  }
  
  li:hover {
    background-color:  #FFF3E2;
  }
  
  body {
    margin: 0;
    padding: 0;
    margin: 0;
    display: flex;
    place-items: center;
    min-width: 320px;
    min-height: 100vh;
    background: linear-gradient(to top, #ffe4c4 0%, #ff9966 100%);
}
  

  li:hover {
    background-color:  #FFF3E2;
  }
  
  input[type="text"],
  button[type="submit"] {
    padding: 0.5rem;
    border: none;
    border-radius: 0.25rem;
    background-color: #f5f5f5;
    font-size: 1rem;
    font-weight: bold;
  }
  
  input[type="text"] {
    width: 100%;
    margin-bottom: 0.5rem;
  }
  
  button[type="submit"] {
    background-color: #333;
    color: #fff;
    cursor: pointer;
    transition: background-color 0.2s ease-in-out;
  }
  
  button[type="submit"]:hover {
    background-color: #555;
  }

  .selesai {
    text-decoration: line-through;
  }

  input[type="checkbox"] {
    margin-right: 0.5rem;
  }

  .container {
    max-width: 600px;
    margin: 0 auto;
    padding: 2rem;
  }
</style>