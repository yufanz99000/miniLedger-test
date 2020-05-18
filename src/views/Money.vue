<template>
    <Layout class-prefix="layout">
        <NumberPad :value.sync="record.amount" @submit="saveRecord"/>
        <Tabs :data-source="typeList" :value.sync ="record.type"/>
        <div class="notes">
            <Notes field-name="备注" placeholder="在这里输入备注"
                   :value="record.notes"
                   @update:value="onUpdateNotes"/>
        </div>
        <Tags @update:value="record.tags = $event"/>
    </Layout>
</template>

<script lang="ts">
    import Vue from 'vue';
    import NumberPad from '@/components/Money/NumberPad.vue';
    import Notes from '@/components/Money/Notes.vue';
    import Tags from '@/components/Money/Tags.vue';
    import {Component} from 'vue-property-decorator';
    import typeList from '@/constants/typeList';
    import Tabs from '@/components/Tabs.vue';

    @Component({
        components: {Tabs, Tags, Notes, NumberPad}
    })
    export default class Money extends Vue {
        get recordList() {
            return this.$store.state.recordList;
        }

        typeList = typeList;

        record: RecordItem = {
            tags: [], notes: '', type: '-', amount: 0
        };

        created() { //在页面加载时
            this.$store.commit('fetchRecords');
        }

        onUpdateNotes(value: string) {
            this.record.notes = value;
        }

        saveRecord() {
            if(!this.record.tags || this.record.tags.length===0) {
              return  window.alert('请至少选择一个标签');
            }
            this.$store.commit('createRecord', this.record);
            if (this.$store.state.createRecordError === null) {
                window.alert('已保存');
                this.record.notes = '';
            }
        }
    }
</script>

<style lang="scss">
    .layout-content {
        /*border: 2px solid red;*/
        display: flex;
        flex-direction: column-reverse;
    }

    .notes {
        padding: 12px 0;
    }
</style>

