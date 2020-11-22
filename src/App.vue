<template>
    <div id="app">
      <Header />
      <Tracker />


    </div>
</template>
    
<script>
import "./assets/style.css"
import Header from './components/Header.vue'
import Tracker from './components/Tracker.vue'
    export default{
      components: {Header, Tracker}
    }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  height: 100vh;
  overflow: hidden;
  background-color: #fff;
}
body{
  margin: 0;
  background-color: #353a5b;
}
</style>
