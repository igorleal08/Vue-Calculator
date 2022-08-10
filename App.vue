<template>
  <div id="app">
    <h1>Calculator!!!</h1>
    <calculator-item />
  </div>
</template>

<script>

import CalculatorItem from "./main/CalculatorItem.vue"

export default {
  name: 'App',
  components: { CalculatorItem }
}
</script>

<style>

@font-face {
  font-family: "Oswald-Regular.ttf";
  src: url("./fonts/Oswald-Regular.ttf");
}

* {
  font-family: "Oswald-Regular", monospace;
}

body {
  margin: 0;
}

#app {
  display: flex;
  flex-direction:  column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;

  color: white;
  background: rgb(83, 105, 118);
  /* background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73)); */

  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>
