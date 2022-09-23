<template>
    <div class="title-search">
        <el-input v-model="input" placeholder="请输入姓名搜索🔍" />
        <el-button type="primary">增加</el-button>
    </div>
</template>
<style lang="less" scoped>
.title-search{
    display: flex;
}
</style>
<script setup>
import { ref } from 'vue'
// 数据
const input = ref('')
</script>