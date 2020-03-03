<template>
  <div class="current-dt" v-if="dt">
    <div class="current-dt-date">{{ dt.date }}</div>
    <div class="current-dt-day">{{ dt.day }}</div>
    <div class="current-dt-time">{{ dt.time }}</div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "currentTime",
  data: () => ({
    dt: null
  }),
  created() {
    this.formatDateTime();
    setInterval(() => {
      this.formatDateTime();
    }, 1e3);
  },
  methods: {
    formatDateTime() {
      const now = moment();
      this.dt = {
        date: now.format("MMMM do, YYYY"),
        day: now.format("dddd"),
        time: now.format("HH:MM:ss")
      };
    }
  }
};
</script>

<style lang="scss" scoped>
.current-dt {
  &-day {
    font-size: 100px;
    font-weight: 100;
  }
  &-time {
    font-weight: 100;
    font-size: 32px;
  }
}
</style>
