<template>
  <div class="app">
    <div class="header container h-100 p-5 mt-2">
      <h1 class="text-center mb-5">Weather Vue</h1>
      <div class="d-flex justify-content-center h-100">
        <div class="searchbar w-50 mx-2">
          <input type="text" class="input form-control" v-model="city" placeholder="Enter a City Name">
        </div>
        <button class="btn btn-primary btn-search">Search <i class="fas fa-search"></i></button>
      </div>
    </div>
    <Weather></Weather>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'

export default {
  name: 'App',
  components: {
    Weather
  },
  data() {
    return {
      city: '',
      showWeather: false
    }
  },
  methods: {
    async fetchWeather() {
      this.showWeather = false;
      await this.$nextTick();
      this.showWeather = true;
    }
  }
}
</script>

<style>
  body {
    background-color: #121212 !important;
  }
  .header {
    background-color: #212730;
    color: #ffffff;
    border-radius: 20px;
  }
  .btn-search {
    background-image: linear-gradient(to right, cyan, magenta);
  }
</style>
