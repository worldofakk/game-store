<template>
  <div id="app">
    <vMainWrapper/>
  </div>
</template>

<script>
import vMainWrapper from "./components/v-main-wrapper"
export default {
  name: 'App',
  components: {
    vMainWrapper,
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 900px;
  margin: 0 auto;
  padding: 0px 30px 0px 30px;
  height: 100vh;
  box-shadow: 0 0 8px 0 #e3e3e3;
}
</style>
