<template>
    <div class="tags">
        <div class="newTag">
            <button @click="createTag">新增标签</button>
        </div>
        <ul class="current">
            <li v-for="tag in tagList" :key="tag.id"
                :class="{selected: selectedTags.indexOf(tag) >= 0}"
                @click="toggle(tag)">{{tag.name}}
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
    // import Vue from 'vue';
    import {Component} from 'vue-property-decorator';
    import {mixins} from 'vue-class-component';
    import TagHelper from '@/mixins/TagHelper';

    @Component
    export default class Tags extends mixins(TagHelper) {

        selectedTags: string[] = [];

        get tagList() {
            return this.$store.state.tagList;
        }

        created() {
            this.$store.commit('fetchTags');
        }

        toggle(tag: string) {
            const index = this.selectedTags.indexOf(tag);
            if (index >= 0) { //点击的时候已经在selectedtags里面了
                this.selectedTags.splice(index, 1);
            } else {
                this.selectedTags.push(tag);
            }
            this.$emit('update:value', this.selectedTags);
        }
    }
</script>

<style lang="scss" scoped>
    @import "~@/assets/styles/helper.scss";

    .tags {
        font-size: 14px;
        padding: 16px;
        display: flex;
        flex-grow: 1;
        flex-direction: column-reverse;
        background: white;

        > .current {
            display: flex;
            flex-wrap: wrap;

            > li {
                background: #d9d9d9;
                $h: 24px;
                height: $h;
                line-height: $h;
                border-radius: ($h/2);
                padding: 0 16px;
                margin-right: 12px;
                margin-top: 4px;

                &.selected {
                    background: orange;
                    color: white;
                }
            }
        }

        > .newTag {
            padding-top: 16px;

            button {
                background: transparent;
                border: none;
                color: #999;
                border-bottom: 1px solid;
                padding: 0 2px;
            }
        }
    }
</style>