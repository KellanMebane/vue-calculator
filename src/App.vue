<template>
  <div id="app">
    <img src="./assets/logo.png">
    <!--router-view/-->
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
export default {
  name: 'App',
  components: {
    Calculator
  }
}

const coolPurple = '#673AB7'
console.log(coolPurple)
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #424242;
  margin-top: 60px;
}
</style>
