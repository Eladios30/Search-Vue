<template>
  <div id="app">
    <!-- <HelloWorld/> -->
    <ChildComponent/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import ChildComponent from './components/ChildComponent.vue';
export default {
  name: 'App',
  components: {
    // HelloWorld,
    ChildComponent
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
</style>
