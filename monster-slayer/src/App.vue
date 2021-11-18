<template>
  <div id="app">
    <MonsterSlayer/>
  </div>
</template>

<script>
import MonsterSlayer from './components/MonsterSlayer.vue'


export default {
  name: 'App',
  components: {
    MonsterSlayer
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
@import './assets/app.css';
@import './assets/foundation.min.css';
</style>
