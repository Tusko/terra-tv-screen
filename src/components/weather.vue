<template>
  <div class="weather">
    <preloader v-if="!weather" />
    <slot v-else>
      <div class="weather-title">{{ weather.weather[0].main }}</div>
      <div class="weather-temp">
        <div class="weather-temp-icon">
          <img
            :src="
              `https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`
            "
          />
        </div>
        <div class="weather-temp-str">
          {{ weather.main.temp }} <sup>0</sup>C
        </div>
      </div>
    </slot>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Weather",
  components: {
    preloader: () => import("./preloader")
  },
  data: () => ({
    weather: null
  }),
  mounted() {
    this.fetchWeather();
  },
  methods: {
    fetchWeather() {
      this.weather = null;
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/weather?q=Khmelnytskyi,ua&APPID=eb9e0756f60584f775d918178eb8da9d&units=metric"
        )
        .then(res => {
          this.weather = res.data;
          setTimeout(this.fetchWeather, 1e4);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.weather {
  white-space: nowrap;
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
