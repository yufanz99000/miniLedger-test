<template>
    <nav>
        <router-link to="/labels" class="item" active-class="selected">
            <Icon class="icon" name="ledger"/>
            标签
        </router-link>

        <router-link to="/money" class="item" active-class="selected">
            <Icon class="icon" name="money"/>
            记账
            </router-link>

        <router-link to="statistics" class="item" active-class="selected">
            <Icon class="icon" name="histogram"/>
            统计
        </router-link>
    </nav>
</template>

<script lang="ts">
    //import x from '@/assets/icons/money.svg';
    //console.log(x);
    export default {
        name: 'Nav'
    };
</script>

<style lang="scss" scoped>
    @import "~@/assets/styles/helper.scss";

    nav{
        @extend %outerShadow;
        display: flex;
        box-shadow: 0 0 3px rgba(0,0,0,0.3);
        flex-direction: row;
        font-size: 12px;
        > .item{
            padding: 2px 0;
            width: 33.33333%;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;

            .icon{
                width:32px; height: 32px;
            }
        }
        > .item.selected{
            color: orange;
        }
    }
</style>