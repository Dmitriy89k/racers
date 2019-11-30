<template>
   <div id="app">
     <h1>Drivers F1</h1>
     <Racers/>
   </div>
</template>

<script>
  import Racers from './components/Racers.vue'

  export default {
    components: {
      Racers
    }
  }
</script>

<style>
  #app {
    max-width: 650px;
    margin: 0 auto;
    text-align: center;
    line-height: 1.4;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  h1 {
    color: lightgray;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
  }
</style>