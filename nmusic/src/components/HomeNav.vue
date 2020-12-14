<template>
  <div class="homenav">
    <div id="nav">
      <router-link to="/">推荐音乐</router-link> |
      <router-link to="/Hot">热歌榜</router-link>|
      <router-link to="/Search">搜索</router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "HomeNav",
};
</script>

<style lang="scss" scoped>
.homenav {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  #nav {
    padding: 30px;
  }

  #nav a {
    font-weight: bold;
    color: #2c3e50;
  }

  #nav a.router-link-exact-active {
    color: #dd001b;
  }
}
</style>
