<template>
  <div id="app">
    <Calculator> </Calculator>
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  data() {
    return {
    
    }
  },
 
  components: {
    Calculator,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
