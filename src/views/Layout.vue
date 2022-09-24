<template>
    <list-exercise />
</template>
<style lang="less" scoped>
.app-layout{
    .new{
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }
    .delete{
        color:#F56C6C;
    }
}
.el-input{
    max-width: 300px;
}
</style>
<script setup>
import ListExercise from '../components/ListExercise.vue'
</script>