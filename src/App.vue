<template>
  <div id="app">
  <Checkers />
<!--    <img alt="Vue logo" class = "desk" src="./assets/desk.jpg">-->
  </div>
</template>

<script>

import Checkers from '@/components/checkers.vue'
export default {
  name: 'App',
  data(){
    return{
      arr: []
    }
  },
  components: {
    Checkers
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
