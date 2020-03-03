<template>
  <div id="app">
    <currentTime />
    <weather />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    currentTime: () => import("./components/currentTime"),
    weather: () => import("./components/weather")
  }
};
</script>
