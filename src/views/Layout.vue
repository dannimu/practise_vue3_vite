<template>
    <div>
        <!-- 标题 -->
         <div class="title-search">
            <el-input v-model="input" placeholder="请输入姓名搜索🔍" />
            <add-popup @dialogForm="dialogForm"/>
        </div>
        <!-- 表格 -->
        <content-section :tableData="tableData"/>
    </div>
</template>
<style lang="less" scoped>
.title-search{
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
}
.el-input{
    width: 200px;
}
</style>
<script setup>
import ContentSection from '../components/ContentSection.vue'
import AddPopup from '../components/AddPopup.vue'
import {ref} from 'vue'
const input = ref('')
const tableData = ref(
    [
        {
            id:'1',
            name: 'Tom',
            email:'1234567@qq.com',
            phone:'222222',
            region: '常州',
        },
        {
            id:'2',
            name: 'Tom',
            email:'1234567@qq.com',
            phone:'222222',
            region: '常州',
        },
        {
            id:'3',
            name: 'Tom',
            email:'1234567@qq.com',
            phone:'222222',
            region: '常州',
        },
        {
            id:'4',
            name: 'Tom',
            email:'1234567@qq.com',
            phone:'222222',
            region: '常州',
        },
    ]
)
function dialogForm(tableData) {
    console.log(tableData);
}
</script>