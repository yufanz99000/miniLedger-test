<!--<script src="main.ts"></script>-->
<template>
  <div id="app">
    <router-view></router-view>
    <hr/>

  </div>
</template>


<style lang="scss">
  body{
    margin:0; padding:0;
    box-sizing: border-box;
  }
   @import "~@/assets/styles/test.scss";
   body {
     background: $pink;
   }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
