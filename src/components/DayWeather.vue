<template>
  <div class="day-tab text-center">
    <div v-if="isLoading" class="loading text-light">Loading...</div>
    <div v-else class="d-flex justify-content-between">
      <div v-for="day in dailyForecast" :key="day.day" class="card mx-3 w-100">
        <div class="py-3">{{ day.day }}</div>
        <div class="py-3"><img :src="day.iconUrl"></div>
        <div class="py-3">{{ day.temp }}&deg; C</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  props: {
    cityName: String,
  },
  data() {
    return {
      isLoading: true,
      dailyForecast: []
    }
  },
  mounted() {
    this.fetchForecast();
  },
  methods: {
    async fetchForecast() {
      const response = await axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${this.cityName}&units=metric&appid=21bfb338ac807e5f3c77d75cf67e65fc`);
      const forecastData = response.data.list;
      console.log(forecastData);
      // Get daily forecast for the next 4 days at almost same time
      for (let i = 0; i < forecastData.length; i++) {
        const forecast = forecastData[i];
        const forecastDate = new Date(forecast.dt_txt);
        // Skip today's date
        const today = new Date();
        if (forecastDate.getDate() === today.getDate()) continue;
        if (forecastDate.getHours() === 9) {
          console.log(forecastDate);
          this.dailyForecast.push({
            day: forecastDate.toLocaleDateString(undefined, { weekday: 'short'}),
            temp: Math.round(forecast.main.temp),
            iconUrl: `http://openweathermap.org/img/w/${forecast.weather[0].icon}.png`
          });
        }
        if (this.dailyForecast.length === 4) break;
      }
      this.isLoading = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
