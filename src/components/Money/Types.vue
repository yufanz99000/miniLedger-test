<template>
    <div>
        <ul class="types">
            <li :class="type === '-' && 'selected'"
                @click="selectType('-')">支出</li>
            <li :class="type === '+' && 'selected'"
                @click="selectType('+')">收入</li>
        </ul>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Prop} from 'vue-property-decorator';

    @Component //使用装饰器
    //告诉ts以下代码是vue的组件，type会被处理成data，selectType会被处理成methods
    export default class Types extends Vue{
        type = '-' //-表示支出， +表示收入

        @Prop(Number) xxx: number | undefined
        //prop告诉vue xxx不是data是prop
        //number告诉vue xxx是个number

        selectType(type: string) {
            if (type !== '-' && type !== '+'){
                throw new Error('type is undefined')
            }
            this.type = type
        }
    }
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