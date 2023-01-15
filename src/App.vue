<template>
  <div class="MainContainer">
    <CalculatorComponent />
  </div>
</template>

<script>
import CalculatorComponent from './components/CalculatorComponent .vue';


export default {
  name: 'App',
  components: {
    CalculatorComponent
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.MainContainer {

  background-color: #272727;
  width: 100vw;
  margin: auto;
}
</style>
