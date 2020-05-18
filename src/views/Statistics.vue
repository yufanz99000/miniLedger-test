<template>
    <div>
        <Layout>
            <Tabs class-prefix="type" :data-source="typeList" :value.sync="type"/>
<!--            <Tabs class-prefix="interval" :data-source="intervalList" :value.sync="interval"/>-->
            <ol v-if="groupedList.length > 0">
                <li v-for="(group, index) in groupedList" :key="index">
                    <h3 class="title">{{beautify(group.title)}}
                        <span>¥{{group.total}}</span>
                    </h3>
                    <ol>
                        <li v-for="item in group.items" :key="item.id" class="record">
                            <span>{{tagString(item.tags)}}</span>
                            <span class="notes">{{item.notes}}</span>
                            <span>¥{{item.amount}}</span>
                        </li>
                    </ol>
                </li>
            </ol>
            <div v-else class="noResult">目前没有记录</div>
        </Layout>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import {Component} from 'vue-property-decorator';
    import Tabs from '@/components/Tabs.vue';
    import typeList from '@/constants/typeList';
    import clone from '@/lib/clone';
    import dayjs from 'dayjs';

    @Component({
        components: {Tabs},
    })

    export default class Statistics extends Vue {
        tagString(tags: Tag[]) {
            return tags.length === 0 ? '无' : tags.map(t=>t.name).join('，');
        }

        beautify(string: string) {
            const day = dayjs(string);
            const now = dayjs();
            if (day.isSame(now, 'day')) {
                return '今天';
            } else if (day.isSame(now.subtract(1, 'day'), 'day')) {
                return '昨天';
            } else if (day.isSame(now.subtract(2, 'day'), 'day')) {
                return '前天';
            } else if (day.isSame(now, 'year')) {
                return day.format('M月D日');
            } else {
                return day.format('YYYY年M月D日');
            }
        }

        get recordList() {
            return (this.$store.state as RootState).recordList;
        }

        get groupedList() {
            const {recordList} = this;

            const newList = clone(recordList)
                .filter(r => r.type === this.type) //分支出和收入
                .sort((a, b) =>
                dayjs(b.createdAt).valueOf() - dayjs(a.createdAt).valueOf());

            if (newList.length === 0) {return [];} //判断filter后的数组长度是否为0

            type Result = { title: string; total?: number; items: RecordItem[] }[]
            const result: Result = [{
                title: dayjs(newList[0].createdAt).format('YYYY-MM-DD'),
                total: 0, //可以不用写因为已经初始化可以是undefined
                items: [newList[0]]
            }];

            for (let i = 1; i < newList.length; i++) {
                const current = newList[i];
                const last = result[result.length - 1];
                if (dayjs(last.title).isSame(dayjs(current.createdAt), 'day')) {
                    last.items.push(current);
                } else {
                    result.push({title: dayjs(current.createdAt).format('YYYY-MM-DD'), items: [current]});
                }
            }
            result.map(group => { //已经分好支出和收入的group
                group.total = group.items.reduce((sum, item) => {
                    console.log(sum);
                    console.log(item);
                    return sum + item.amount
                }, 0)
            })
            return result;
        }

        beforeCreate() {
            this.$store.commit('fetchRecords');
        }

        type = '-';
        // interval = 'day';
        // intervalList = intervalList;
        typeList = typeList;
    }


</script>

<style lang="scss" scoped>
    .noResult{
        text-align: center;
        padding: 16px;
    }
    ::v-deep {
        .type-tabs-item {
            background: white;
            &.selected {
                background: orange;
                &::after {
                    display: none;
                }
            }
        }
        .interval-tabs-item {
            height: 48px;
        }
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