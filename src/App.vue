<template>
  <div id="app">
    <LightOnBoard :lightOnCount="4" :size="5" />
  </div>
</template>

<script>
import LightOnBoard from "./components/LightOnBoard.vue";

export default {
  name: "App",
  components: {
    LightOnBoard,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 1rem 0 0 0;
}
</style>
