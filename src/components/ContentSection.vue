<template>
    <el-table 
    :data="tableData" 
    class="content-section" 
    border
    ref="multipleTableRef"
    @selection-change="handleSelectionChange"
    > 
        <el-table-column type="selection" width="55" />
        <!-- <el-table-column prop="id" label="Id" width="100" /> -->
        <el-table-column prop="name" label="姓名" width="80" />
        <el-table-column prop="email" label="邮箱" width="150" />
        <el-table-column prop="phone" label="电话" width="150" />
        <el-table-column prop="region" label="地址" width="100" />
        <el-table-column label="操作" width="120">
        <template #default>
            <el-button link type="primary" size="small" class="red" 
            @click="handleClick"
            style="color:#F56C6C"
            >删除</el-button>
            <el-button link type="primary" size="small">编辑</el-button>
        </template>
        </el-table-column>
    </el-table>
</template>
<style lang="less" scoped>
</style>
<script>
import {ref, toRefs} from 'vue'
export default {
    props:{
        tableData:Object
    },
    setup(props) {
        // 数据
        const {tableData} = toRefs(props)
        const multipleSelection = ref([])
        // 方法
        function handleClick() {
            console.log('click');
        } 
        const handleSelectionChange = (val) => {
            multipleSelection.value = val
            console.log(val);
        }
        return{
            tableData,multipleSelection,handleClick,handleSelectionChange
        }
    }
}
</script>