<template>
    <div class="tags">
        <div class="newTag">
            <button>新增标签</button>
        </div>
        <ul class="current">
            <li>衣</li>
            <li>食</li>
            <li>住</li>
            <li>行</li>
            <li>购物</li>
            <li>健康</li>
            <li>教育</li>
            <li>娱乐</li>
        </ul>
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Tags'
    };
</script>

<style lang="scss" scoped>
    @import "~@/assets/styles/helper.scss";
    .tags {
        font-size: 14px;
        padding: 16px;
        display: flex;
        flex-grow: 1;
        flex-direction: column-reverse;
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