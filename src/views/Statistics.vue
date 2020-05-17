<template>
    <div>
        <Layout>
            <Tabs class-prefix="type" :data-source="typeList" :value.sync="type"/>
<!--            <Tabs class-prefix="interval" :data-source="intervalList" :value.sync="interval"/>-->
            <ol>
                <li v-for="(group, index) in result" :key="index">
                    <ol>
                        <li v-for="item in group.items" :key="item.id" class="record">
                            <span>{{tagString(item.tags)}}</span>
                            <span class="notes">{{item.notes}}</span>
                            <span>¥{{item.amount}}</span>
                        </li>
                    </ol>
                </li>
            </ol>
        </Layout>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import {Component} from 'vue-property-decorator';
    import Tabs from '@/components/Tabs.vue';
    import intervalList from '@/constants/intervalList';
    import typeList from '@/constants/typeList';
    import clone from '@/lib/clone';
    @Component({
        components: {Tabs},
    })

    export default class Statistics extends Vue {
        get recordList(){
            return (this.$store.state as RootState).recordList;
        }

        get result() {
            const {recordList} = this;
            type Items = RecordItem[];
            type HashTableValue = { title: string; items: Items};
            const hashTable: {[key: string]: HashTableValue} = {};

            for (let i=0; i< recordList.length; i++) {
                const [date, time] = recordList[i].createdAt!.split('T')
                hashTable[date] = hashTable[date] || {title:date, items:[]}
                hashTable[date].items.push(recordList[i])
            }
            return hashTable;
        }

        beforeCreate() {
            this.$store.commit('fetchRecords');
        }
        type = '-';
        interval = 'day';
        intervalList = intervalList;
        typeList = typeList;
    }


</script>

<style lang="scss" scoped>
    ::v-deep .type-tabs-item {
        background: white;
        &.selected {
            background: orange;
            &::after { //如果选中取消下划线
                display: none;
            }
        }
    }
    ::v-deep .interval-tabs-item {
        height: 48px;
    }
    %item {
        padding: 8px 16px;
        line-height: 24px;
        display: flex;
        justify-content: space-between;
        align-content: center;
    }
    .title {
        @extend %item;
    }
    .record {
        background: white;
        @extend %item;
    }
    .notes {
        margin-right: auto;
        margin-left: 16px;
        color: #999;
    }

</style>