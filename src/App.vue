<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">-->
<!--  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <FruitsList msg="Welcome to Your Vue.js App"/>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import FruitsList from "@/components/FruitsList";

export default {
  name: 'App',
  components: {
    FruitsList,
    // HelloWorld
  }
}
</script>

<style>
body{
  background-color: #F2EEEB;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
