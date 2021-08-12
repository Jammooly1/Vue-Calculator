<template>
  <div class="header">
    <h1 class="display-4">Jamal's Vue Calculator</h1>
  </div>
  <calculator></calculator>
</template>

<script>
import Calculator from './components/Calculator.vue'
export default {
  name: 'App',
  components: {Calculator} 
}
</script>

<style scope>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 40px; 
}

h1{
  font-family:monospace;
  color: #234
}

.header {
  max-width: 500px;
  margin: 0 auto;
  background-color: #3fb984;
  border-radius: 5px;
  box-shadow: gray .5px .5px .5px .5px;
}

</style>
