<template>
  <div id="app">
    <img alt="logo" src="./assets/logo.png">
    <HelloWorld msg="Basics with VueJS"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  components: {
    HelloWorld,
  },
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Roboto');

  #app {
    text-align: center;
    color: #2C3E50;
    margin-top: 60px;
    font-family: 'Roboto';

    img {
      height: 200px;
      max-width: 100%;
    }
  }
</style>
