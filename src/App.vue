<template>
  <main>
    <div id="app">
      <Calculator />
    </div>
  </main>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

main {
  min-height: 100vh;

  background-image: url("./assets/blue-bg.jpg");
  background-size: cover;
  background-position: bottom;
}
</style>
