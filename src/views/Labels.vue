<template>
    <Layout>
        <div class="tags">
            <router-link class="tag" v-for="tag in tags" :key="tag.id"
                         :to="`/labels/edit/${tag.id}`">
                <span>{{tag.name}}</span>
                <Icon name="right"/>
            </router-link>
        </div>
        <div class="createTag-wrapper">
            <Button class="createTag" @click.native="createTag">新建标签</Button>
        </div>
    </Layout>

</template>

<script lang="ts">
    import {Component} from 'vue-property-decorator';
    import Button from '@/components/Button.vue';
    import {mixins} from 'vue-class-component';
    import TagHelper from '@/mixins/TagHelper';

    @Component({
        components: {Button}
    })
    export default class Labels extends mixins(TagHelper) {
        get tags() {
            return this.$store.state.tagList;
        }

        beforeCreate() {
            this.$store.commit('fetchRecords');
        }

        // createTag() { 因为在mixins里面引入，这里不需要写
        //     const name = window.prompt('请输入标签名');
        //     if (!name) { return window.alert('标签名不能为空'); }
        //     this.$store.commit('createTag', name);
        // }
    }
</script>

<style lang="scss" scoped>
    .tags {
        background: white;
        font-size: 16px;
        padding-left: 16px;

        > .tag {
            min-height: 44px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid #e6e6e6;

            svg {
                color: orange;
                margin-right: 16px;
                width: 24px;
                height: 24px;
            }
        }
    }

    .createTag {
        background: orange;
        border-radius: 6px;
        color: white;
        border: none;
        height: 40px;
        padding: 0 16px;

        &-wrapper {
            text-align: center;
            padding: 16px;
            margin-top: 44-16px;
        }
    }
</style>