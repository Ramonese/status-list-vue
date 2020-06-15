<template>
  <div id="app">
    <StatusItem currentStatus="test" />
  </div>
</template>

<script>
import StatusItem from "./components/StatusItem.vue";

export default {
  name: "App",
  components: {
    StatusItem
  }
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
