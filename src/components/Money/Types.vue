<template>
    <div>
        <ul class="types">
            <li class="selected">支出</li>
            <li>收入</li>
        </ul>
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Types'
    };
</script>

<style lang="scss" scoped>
    @import "~@/assets/styles/helper.scss";

    .types {
        /*background: PapayaWhip;*/
        display: flex;
        text-align: center;
        font-size: 24px;

        > li {
            width: 50%;
            /*line-height: 60px;*/
            height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;

            &.selected {
                &::after {
                    content: '';
                    position: absolute;
                    bottom: 0;
                    left: 0;
                    width: 100%;
                    height: 4px;
                    background: orange;
                }
            }
        }
    }
</style>