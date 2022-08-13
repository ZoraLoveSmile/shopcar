<template>
  <div id="app">
     <indexs></indexs>
  </div>
</template>

<script>
import indexs from "./components/indexs.vue";

export default {
  name: "App",
  components: {
    indexs
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
  margin-top: 60px;
}
</style>
