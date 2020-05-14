<template>
    <div>
        <ul class="types">
            <li :class="value === '-' && 'selected'"
                @click="selectType('-')">支出</li>
            <li :class="value === '+' && 'selected'"
                @click="selectType('+')">收入</li>
        </ul>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Prop, Watch} from 'vue-property-decorator';

    @Component //使用装饰器
    export default class Types extends Vue{
        //type = '-' //-表示支出， +表示收入
        @Prop() readonly  value!: string
        //告诉value去读取money.vue里record.type
        selectType(type: string) {
            if (type !== '-' && type !== '+'){
                throw new Error('type is undefined')
            }
            this.$emit('update:value', type)
        }
        // @Watch('type')
        // onTypeChanged(value: string) {
        //     this.$emit('update-value', value)
        // }
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