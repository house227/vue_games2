<template>
  <body>
      <div id="app">
        <table id="table">
          <tr>
            <td><square v-bind:square="square"/></td>
            <td></td>
            <td></td>
          </tr>

          <tr>
            <td></td>
            <td></td>
            <td></td>
          </tr>

          <tr>
            <td></td>
            <td></td>
            <td></td>
          </tr>
        </table>
      </div>
  </body>
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
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
#table{
      margin:0 auto;
      border-collapse: collapse;
      border: 3px solid #ccc ;
}

#table td{
        height: 200px;
        width: 200px;
        text-align: center;
        font-size: 100px;
        line-height: 200px;
        border: 1px solid black;
        margin: 0;
        cursor: pointer;
        }
</style>
