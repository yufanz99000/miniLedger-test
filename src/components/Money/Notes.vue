<template>
    <div>
        <label class="notes">
            <span class="name">{{this.fieldName}}</span>
            <input type="text"
                   :value="value"
                  @input="onValueChanged($event.target.value)"
                   :placeholder="this.placeholder">
        </label>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Prop} from 'vue-property-decorator'

    @Component
    export default class Notes extends Vue{
        @Prop({default: ''}) readonly value!: string;
        @Prop({required: true}) fieldName!: string;
        @Prop() placeholder?: string;

        onValueChanged(newVal: string, oldVal: string){
            this.$emit('update:value', newVal)
        }
    }
</script>

<style lang="scss" scoped>
    @import "~@/assets/styles/helper.scss";
    .notes {
        font-size: 14px;
        padding-left: 16px;
        display: flex;
        align-items: center;

        .name {
            padding-right: 16px;
        }

        input {
            height: 40px;
            flex-grow: 1;
            background: transparent;
            border: none;
            padding-right: 16px;

        }
    }
</style>