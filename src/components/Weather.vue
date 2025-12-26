<template>
  <div class="container p-0">
    <div class="d-flex mb-2">
      <div class="card main-div w-100">
        <div class="p-3">
          <h2 class="mb-1 day">Today</h2>
          <p class="text-light date">{{date}}</p>
          <small>{{time}}</small>
          <h2 class="place"><i class="fas fa-location me-1"></i> {{ cityName }}, <small>{{country}}</small></h2>
          <div class="temp">
            <h1 class="weather-temp">{{temperature}}&deg;</h1>
            <h2 class="text-light">{{description}} <img :src="iconUrl" alt="Weather Icon" class="bg-light rounded rounded-2"></h2>
          </div>
        </div>
      </div>
      <div class="card card-2 w-100">
        <table class="m-4">
          <tbody>
            <tr>
              <th>Humidity</th>
              <td>{{humidity}}%</td>
            </tr>
            <tr>
              <th>Wind Speed</th>
              <td>{{windSpeed}} m/s</td>
            </tr>
            <tr>
              <th>Sea Level</th>
              <td>{{seaLevel}}</td>
            </tr>
          </tbody>
        </table>
        <DayWeather></DayWeather>
        <div id="chg_btn_div" class="d-flex justify-content-center m-3">
          <form action="">
            <input type="button" value="Change Location" class="btn change-btn btn-primary">
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DayWeather from './DayWeather.vue';
import axios from 'axios';

export default {
  name: 'theWeather',
  components: {
    DayWeather
  },
  props: {
    city: String,
  },
  data() {
    return {
      temperature: null,
      description: null,
      iconUrl: null,
      date: null,
      time: null,
      humidity: null,
      windSpeed: null,
      seaLevel: null,
      cityName: null,
      country: null,
    }
  },
  async created() {
    const apiString = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=21bfb338ac807e5f3c77d75cf67e65fc`;
    // console.log(apiString);
    const response = await axios.get(apiString);
    const weatherData = response.data;
    console.log(weatherData);
    this.temperature = Math.round(weatherData.main.temp);
    this.description = weatherData.weather[0].description;
    this.iconUrl = `http://openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
    // console.log(this.iconUrl);
    this.date = new Date();
    this.time = this.date.toLocaleTimeString();
    this.date = this.date.toLocaleDateString();
    this.humidity = weatherData.main.humidity;
    this.windSpeed = weatherData.wind.speed;
    this.seaLevel = weatherData.main.sea_level || 'N/A';
    this.cityName = weatherData.name;
    this.country = weatherData.sys.country;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body {
    background-color: #343d4b;
  }
  .weather-temp {
    margin: 0;
    font-size: 4em;
    font-weight: 700;
  }
  h2.mb-1.day {
    font-size: 3rem;
    font-weight: 400;
  }
  .card {
    border-radius: 20px;
    color: #ffffff;
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>
