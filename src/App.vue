<template>
  <div id="app">
    <square v-bind:square="square"/>
  </div>
</template>

<script>
import square from './components/square.vue'
export default {
  name: 'App',
  components: {
    square
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

/* .square{
        height: 200px;
        width: 200px;
        text-align: center;
        font-size: 100px;
        line-height: 200px;
        border: 1px solid black;
        margin: 0;
        } */
</style>
