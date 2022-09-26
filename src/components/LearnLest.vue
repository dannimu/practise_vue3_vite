<template>
    <div class="learn-lest">
        <h2>列表显示</h2>
        <!-- 搜索输入框+新增按钮 -->
        <div class="header">
            <el-input v-model="input" placeholder="用户名" class="search"/>
            <el-button type="primary" @click="dialogFormVisible = true">新增</el-button>
            <!-- 弹框 -->
            <el-dialog v-model="dialogFormVisible" :title="ShippingAddress==='add'?'新增':'编辑'">
                <el-form :model="form">
                    <!--弹框 日期 -->
                    <el-form-item label="日期" :label-width="formLabelWidth">
                        <el-input v-model="form.date" autocomplete="off" />
                    </el-form-item>
                    <!--弹框 姓名 -->
                    <el-form-item label="姓名" :label-width="formLabelWidth">
                        <el-input v-model="form.name" autocomplete="off" />
                    </el-form-item>
                    <!--弹框 状态 -->
                    <el-form-item label="状态" :label-width="formLabelWidth">
                        <el-input v-model="form.state" autocomplete="off" />
                    </el-form-item>
                    <!--弹框 地址 -->
                    <el-form-item label="地址" :label-width="formLabelWidth">
                        <el-input v-model="form.address" autocomplete="off" />
                    </el-form-item>
                    <!--弹框 城市 -->
                    <el-form-item label="城市" :label-width="formLabelWidth">
                        <el-select v-model="form.city" placeholder="北京">
                            <el-option label="北京" value="shanghai" />
                            <el-option label="上海" value="beijing" />
                        </el-select>
                    </el-form-item>
                </el-form>
                <template #footer>
                    <span class="dialog-footer">
                        <el-button @click="dialogFormVisible = false">取消</el-button>
                        <el-button type="primary" @click="dialogFormVisible = false">确定</el-button>
                    </span>
                </template>
            </el-dialog>
        </div>
        <!-- 表格 -->
        <el-table 
        ref="multipleTableRef"
        :data="tableData"
        style="width: 100%"
        @selection-change="handleSelectionChange"
        >
            <el-table-column type="selection" width="55" />
            <el-table-column fixed prop="date" label="日期" width="100" />
            <el-table-column prop="name" label="姓名" width="80" />
            <el-table-column prop="state" label="状态" width="120" />
            <el-table-column prop="city" label="城市" width="120" />
            <el-table-column prop="address" label="地址" width="300" />
            <el-table-column fixed="right" label="操作" width="120">
            <template #default>
                <el-button link type="primary" size="small" @click="handleClick" class="delete">删除</el-button>
                <el-button link type="primary" size="small">编辑</el-button>
            </template>
            </el-table-column>
        </el-table>
    </div>
    <hr>
</template>
<style lang="less" scoped>
.learn-lest{
    .header{
        display: flex;
        justify-content: space-between; 
        .search{
            width: 300px;
            margin-bottom: 20px;
        }
    }
    .delete{
        color: #F56C6C;
    }
}
</style>
<script setup>
import { ref,reactive ,inject,onMounted} from 'vue'
//inject方法注入  请求后端数据
const $http = inject("$http")
// 表格内容
const tableData = ref([])

// 变量
// 搜索输入框
const input = ref('')
// 多选框选中状态
const multipleSelection = ref([])
// 弹框展开或者关闭
const dialogFormVisible = ref(false)
// 弹框新增列表内容
const form = ref([])
// 弹框内容属性的宽度
const formLabelWidth = ref('150px')
// 弹框列表标题（新增或者编辑）
const ShippingAddress = ref('add')

// 方法
// 单选删除
function handleClick(params) {
    console.log('click单选删除')
}
// 多选框
function handleSelectionChange(val) {
    multipleSelection.value = val
}

// 请求表格内容 (方法)
const getData = async() =>{
    const {data:res} = await $http.post('http://127.0.0.1:3000/yinan2',{})
    tableData.value = res
    console.log(res);
}  

// 调用方法
onMounted(()=>{
    getData()
})
</script>