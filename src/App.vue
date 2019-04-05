<template>
  <b-container fluid>
    <div id="app" class="fullScreen">
      <app-home></app-home>
    </div>
  </b-container>
</template>

<script>
import Home from "./components/Home.vue";
export default {
  name: "app",
  components: {
    appHome: Home
  }
};
</script>

<style>
</style>
