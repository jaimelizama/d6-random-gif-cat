<template>
  <div id="app">
    <h2 class="my-4">Random Gif Cat</h2>
    <div>
      <form @submit.prevent="searchMyCat">
        <div class="form-options py-2">
          <div class="form-text">
            <div class="row">
              <div class="col-6 text-right pr-0">
                <label>Titulo:</label>
              </div>
              <div class="col-6 text-left pl-0">
                <input
                  type="text"
                  v-model="formTitle"
                  required
                  placeholder="Escriba un titulo"
                />
              </div>
            </div>
          </div>
          <div class="form-filter mt-2">
            <div class="row d-flex">
              <div class="col-6 text-right pr-0">
                <label>Filtro:</label>
              </div>
              <div class="col-6 text-left pl-0">
                <select v-model="formFilter" required>
                  <option disabled selected value="">Elige un filtro</option>
                  <option value="blur">Blur</option>
                  <option value="mono">Mono</option>
                  <option value="sepia">Sepia</option>
                  <option value="negative">Negative</option>
                  <option value="paint">Paint</option>
                  <option value="pixel">Pixel</option>
                </select>
              </div>
            </div>
          </div>
          <div class="form-color mt-2">
            <div class="row">
              <div class="col-6 text-right pr-0">
                <label>Color:</label>
              </div>
              <div class="col-2 text-left pl-0">
                <select v-model="formColor" required>
                  <option disabled selected value="">Elige un color</option>
                  <option value="white">Blanco</option>
                  <option value="red">Rojo</option>
                  <option value="blue">Azul</option>
                  <option value="yellow">Amarillo</option>
                  <option value="green">Verde</option>
                </select>
              </div>
              <div class="col-4 text-right pr-0">
                <div
                  class="ml-2 circle"
                  :style="{
                    background:
                      formColor === formColor ? formColor : 'transparent'
                  }"
                ></div>
              </div>
            </div>
          </div>
          <div class="form-size mt-2">
            <div class="row justify">
              <div class="col-6 text-right pr-0">
                <label>Tamaño:</label>
              </div>
              <div class="col-6 text-left pl-0">
                <input
                  type="number"
                  v-model.number="formSize"
                  required
                  placeholder="Ingrese un tamaño"
                />
              </div>
            </div>
          </div>
        </div>

        <button class="mt-2" type="submit">Obtener mi gatito</button>
      </form>
      <!-- Revisar si está leyendo los datos ingresados -->
      <!-- {{ formTitle }} {{ formFilter }} {{ formColor }} {{ formSize }} -->
    </div>
    <img class="mt-3" :src="catUrl" />
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    formTitle: '',
    formFilter: '',
    formColor: '',
    formSize: '',
    catUrl: ''
  }),
  methods: {
    searchMyCat() {
      console.log('submit')
      console.log(this.catUrl)
      this.fetchCatApi()
    },
    fetchCatApi() {
      fetch(
        `https://cataas.com/cat/gif/says/${this.formTitle}?size=${this.formSize}&color=${this.formColor}&filter=${this.formFilter}`
      )
        .then((response) => response.blob())
        .then((blob) => {
          let objectUrl = URL.createObjectURL(blob)
          this.catUrl = objectUrl
        })
    }
  }
}
</script>

<style>
html {
  background: #add9e6;
}

.form-options {
  background: #f0807f;
}

.form-color select {
  display: flex;
  vertical-align: middle;
  height: 30px;
  display: grid;
}

.circle {
  position: relative;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: #add9e6;
}
</style>
