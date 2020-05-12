<template>
  <div id="app">
    <router-view></router-view>
    <hr/>

  </div>
</template>

<style lang="scss">
  @import "~@/assets/styles/reset.scss";
  @import "~@/assets/styles/helper.scss";

   body {
     background: lightblue;
     line-height: 1.5;
     font-family: $font-hei;
     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     color: #333;
   }

#nav {
  padding: 30px;
  &.router-link-exact-active {
      color: #42b983;
    }
  }

</style>
