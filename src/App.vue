<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/join">Join</router-link>
      <router-link to="/login">Login</router-link>
    </div>
    <!-- <HereMap
        appId="APP-ID-HERE"
        appCode="APP-CODE-HERE"
        lat="37.7397"
        lng="-121.4252"
        width="100%"
        height="835px"
    /> -->

    <router-view/>
  </div>
</template>

<script>
  import HereMap from "./components/HereMap.vue"

  export default {
    name: 'app',
    components: {
      HereMap,
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
</style>
