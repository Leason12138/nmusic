<template>
  <div id="app">
   <HomeNav></HomeNav>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/Hot">Hot</router-link>
    </div>
    <router-view/> -->
  </div>
</template>
<script>
import HomeNav from './components/HomeNav.vue'

export default {
      components: {
        HomeNav
    },
}
</script>
<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


</style>
