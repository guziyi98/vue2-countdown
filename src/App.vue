<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <Box /> -->
  </div>
</template>

<script>
// import Box from 'views/box.vue'
import { getDataType } from 'js-utils-gzy'
export default {
  name: 'App',
  components: {
    // Box
  },
  mounted () {
    console.log(getDataType(1))
    console.log(getDataType('1'))
    console.log(getDataType({a: 1}))
    console.log(getDataType([1]))
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
  margin-top: 60px;
}
</style>
