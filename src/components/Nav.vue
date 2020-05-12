<template>
    <div class="nav">
        <router-link to="/money">
            <Icon name="ledger"/>
            账本
        </router-link>|

        <router-link to="/labels">
            <Icon name="money"/>
            记账
            </router-link>|

        <router-link to="statistics">
            <Icon name="histogram"/>
            统计
        </router-link>
    </div>
</template>

<script lang="ts">
    //import x from '@/assets/icons/money.svg';
    //console.log(x);
    export default {
        name: 'Nav'
    };
</script>

<style lang="scss" scoped>
    .nav{
        border: 1px solid red;
    }
</style>