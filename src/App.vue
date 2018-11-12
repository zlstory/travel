<template>
  <div id="app">
    <keep-alive exclude="Detail">
      <router-view/>
      <!-- 页面中当前路由所显示的地址 -->
    </keep-alive>
  </div>
</template>

<script>
  export default {
    name: "App"
  }
</script>

<style>
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
</style>
