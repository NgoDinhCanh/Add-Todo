<template>
  <div id="app">
    <Header />
    <Todies />
  </div>
</template>

<script>
import Header from "./components/Header";
import Todies from "./components/Todies";

export default {
  name: "App",
  components: {
    Header,
    Todies,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
