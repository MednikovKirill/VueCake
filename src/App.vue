<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <ViewHelWord />
    <PipCake />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ViewHelWord from './components/ViewHelWord.vue'
import PipCake from './components/PipCake.vue'

export default {
  name: 'app',
  components: {
    HelloWorld, 
    ViewHelWord,
    PipCake
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
