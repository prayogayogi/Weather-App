<template>
  <div id="app">
    <div class="container">
    <h1>Weather App</h1>
      <div class="row justify-content-center">
        <div class="col-11 mt-2">
          <div class="search">
            <input type="text" name="Search" v-model="cari" autofocus class="form-control" @keyup.enter="dataSuhu" placeholder="Masukan Nama Negara.!">
          </div>
        </div>
      </div>
      <div class="row mt-3" v-if="typeof suhu.main != 'undefined'">
        <div class="col">
          <h4 class="lokasi">{{ suhu.name }}, {{ suhu.sys.country }}</h4>
          <p class="tanggal">{{ dat }}</p>
          <h2 class="suhu">{{ Math.round(suhu.main.temp) }}'C</h2>
          <h3 class="status">{{ suhu.weather[0].main }}</h3>
        </div>
      </div>
      <div class="not" v-else>
        <p class="mt-4">Silahkan Masukan Negara Yang Anda Inggin Anda Cari.!</p>
      </div>
    </div>
  </div>
</template>

<script>
import bootstrap from 'bootstrap/dist/css/bootstrap.css'
import axios from 'axios'

export default {
  name:"judul",bootstrap,
  data() {
    return {
      urlApi: 'https://api.openweathermap.org/data/2.5/',
      apiKey: '8a5a0fc6ec28d0edc29b6c280f4ffca7',
      cari: '',
      suhu:{},
      dat: ''
    }
  },
  methods:{
    dataSuhu (el) {
      if(el.key == 'Enter'){
        axios.get(`${this.urlApi}weather?q=${this.cari}&units=metric&APPID=${this.apiKey}`)
        .then(res => {
          this.suhu = res.data
        })
      }
      this.dat = new Date().toLocaleString()
      this.cari = ''
    }
  }
}
</script>

<style scoped>
.container{
  border: 5px solid #334756;
  width: 20%;
  padding: 20px;
  border-radius: 35px;
}
</style>
