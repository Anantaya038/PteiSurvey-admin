<template>
  <div id="app">   
  
    <router-view></router-view>
  </div>
</template>

<script>
import MyComponent from './components/MyComponent.vue'

export default {
  name: 'app',
  components: {
    MyComponent
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Lato');
#app {
 font-family: 'Lato', sans-serif;
  background-color: rgb(255, 255, 255);
 
}
</style>
