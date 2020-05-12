<template>
    <div class="nav-wrapper">
        <div class="content">Labels.vue</div>
        <Nav></Nav>
    </div>
</template>

<script lang="ts">

  export default {
    name: 'Labels',

  };
</script>

<style lang="scss" scoped>
    .nav-wrapper{
        border: 3px solid white;
        display: flex;
        flex-direction: column;
        height: 100vh;
    }
    .content{
        overflow: auto;
        flex-grow: 1;
    }
</style>