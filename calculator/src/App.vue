<template>
  <div id="app">
    <h1>Calculator</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./main/Calculator.vue";

export default {
  components: { Calculator },
};
</script>

<style>
@font-face {
  font-family: "RobotoMono";
  src: url("./fonts/RobotoMono-Thin.ttf");
}

* {
  font-family: "RobotoMono", monospace;
}

body {  
  background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73));
  margin: 0;
}

#app {
  align-content: center;
  align-items: center;
  color: #fff;
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  text-align: center;
}
</style>
