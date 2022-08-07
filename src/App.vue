<template>
  <header style="background:#26272b">
      <nav class="navbar navbar" style="color: white;">
        <a class="navbar-brand" href="#">
        <img src="./assets/pg.png" padding-left="200" width="100" height="30" class="d-inline-block align-top" alt="">
          Prueba Final - Solvex
        </a>
      </nav>
    </header>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
