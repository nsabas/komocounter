<template>
  <h1>Komo Counter</h1>
  <div></div>
  <Game/>
</template>

<script>
import Game from './components/Game.vue'

export default {
  name: 'App',
  components: {
    Game
  }
}
</script>

<style>
h1 {
  font-family: 'Montserrat', sans-serif;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* just to align verticaly..*/
  position: fixed;
  top: 35%;
  left: 50%;
  transform: translate(-50%, -50%);
}
body {

  background-color: #43BCCD;
}
</style>
