<template>
  <div class="weather">
    <div class="weather-title">{{ weather.weather[0].main }}</div>
    <div class="weather-temp">
      <div class="weather-temp-icon">
        <img
          :src="
            `https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`
          "
        />
      </div>
      <div class="weather-temp-str">{{ weather.main.temp }} <sup>0</sup>C</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Weather",
  data: () => ({
    weather: null
  }),
  created() {
    this.fetchWeather();
  },
  methods: {
    fetchWeather() {
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/weather?q=Khmelnytskyi,ua&APPID=eb9e0756f60584f775d918178eb8da9d&units=metric"
        )
        .then(res => {
          this.weather = res.data;
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.weather {
  text-align: right;
  &-temp {
    align-items: center;
    font-size: 100px;
    font-weight: 100;
    display: flex;
    &-icon {
      margin-right: 20px;
      flex-basis: 100px;
    }
    &-str {
      flex: 1;
    }
  }
}
</style>
