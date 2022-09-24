<template>
    <div class="app-layout">
        <!-- 标题 -->
        <h2>列表demo</h2>
        <!-- 搜索框+新增按钮 -->
        <div class="new">
            <el-input v-model="input" placeholder="请搜索姓名" />
            <div>
                <el-button type="danger" @click="batchDeletion" v-if="multipleSelection.length>1">批量删除</el-button>
                <el-button type="primary" @click="dialogFormVisible = true">增加</el-button>
            </div>
            <el-dialog v-model="dialogFormVisible" :title="dialogType==='add'?'新增':'编辑'">
                <el-form :model="form">
                    <el-form-item label="姓名" :label-width="formLabelWidth">
                        <el-input v-model="form.name" autocomplete="off" />
                    </el-form-item>
                    <el-form-item label="电话" :label-width="formLabelWidth">
                        <el-input v-model="form.phone" autocomplete="off" />
                    </el-form-item>
                    <el-form-item label="邮箱" :label-width="formLabelWidth">
                        <el-input v-model="form.mail" autocomplete="off" />
                    </el-form-item>
                    <el-form-item label="状态" :label-width="formLabelWidth">
                        <el-input v-model="form.state" autocomplete="off" />
                    </el-form-item>
                    <el-form-item label="城市" :label-width="formLabelWidth">
                        <el-select v-model="form.city" placeholder="北京">
                        <el-option label="北京" value="shanghai" />
                        <el-option label="深圳" value="beijing" />
                        </el-select>
                    </el-form-item>
                </el-form>
                <template #footer>
                    <span class="dialog-footer">
                        <el-button type="primary" @click="dialogForm">确认</el-button>
                    </span>
                </template>
            </el-dialog>
        </div>
        <!-- 表格 -->
        <el-table 
        :data="tableData" 
        style="width: 100%"
        ref="multipleTableRef"
        @selection-change="handleSelectionChange"
        >
            <el-table-column type="selection" width="55" />
            <el-table-column prop="id" label="ID" width="120" />
            <el-table-column prop="name" label="姓名" width="120" />
            <el-table-column prop="phone" label="电话" width="120" />
            <el-table-column prop="city" label="城市" width="120" />
            <el-table-column prop="mail" label="邮箱" width="200" />
            <el-table-column prop="state" label="状态" width="120" />
            <el-table-column fixed="right" label="操作" width="120">
                <template #default="scope">
                    <!-- (scope.row)为当前选中的数据 -->
                    <el-button link type="primary" size="small" class="delete" @click.prevent="deleteRow(scope.row)">删除</el-button>
                    <el-button link type="primary" size="small" @click="contentEdit(scope.row)">编辑</el-button>
                </template>
            </el-table-column>
        </el-table>
    </div>
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
import { ref ,reactive} from 'vue'
const input = ref('')
// 选中状态
const multipleSelection = ref([])
// 弹框展开或关闭
const dialogFormVisible = ref(false)
//弹框里面的输入框 为对象的形式
const form = ref({})
// 弹框里面属性占用的宽度
const formLabelWidth = ref('140px')
// 新增和编辑用同一个弹框，默认是新增弹框
const dialogType = ref('add')
//表格展示的内容 为对象的形式
const tableData = reactive(
    [
        {
        id:'1',
        name: 'Tom1',
        phone: '7979890',
        city: '北京',
        mail: '12345@qq.com',
        state: '待定',
        },
        {
        id:'2',
        name: 'Tom2',
        phone: '7979890',
        city: '北京',
        mail: '12345@qq.com',
        state: '待定',
        },
        {
        id:'3',
        name: 'Tom3',
        phone: '7979890',
        city: '北京',
        mail: '12345@qq.com',
        state: '待定',
        },
        {
        id:'4',
        name: 'Tom4',
        phone: '7979890',
        city: '北京',
        mail: '12345@qq.com',
        state: '待定',
        },
    ]
)

//选中状态  val为框架固定用法
const handleSelectionChange = (val) => {
    // multipleSelection.value = val
    // 默认为不选中的状态
    multipleSelection.value = []
    // forEach()循环遍历数组或集合中的元素。
    //将新的选中内容，push到multipleSelection选中数组里面
    val.forEach(item => {
        multipleSelection.value.push(item.id)
    });
    // console.log(multipleSelection.value);
    // console.log('2222',val);
}

//新增
function dialogForm(params) {
    dialogFormVisible.value = false
    // 把form里面的数据push到tableData里
    tableData.push({
        id:tableData.length + 1,
        //将form里面新增的内容push到tableData数组列表里面
        ...form.value
    })
    console.log(tableData);
}

//单选删除    需要通过ID确定需要删除的内容
function deleteRow(id) {
    // 1.通过id获取到条目对应的 索引值
    const index = tableData.findIndex(item => item.id === id)
    // 2.通过索引值进行删除对应条目
    tableData.splice(index,1)
}
//批量删除
function batchDeletion() {
    // forEach()循环遍历数组或集合中的元素。
    multipleSelection.value.forEach(id => {
        deleteRow(id = id)
    });
    //删除完成之后剩余的为没选中状态  （可有可无）
    multipleSelection.value = []
}

//编辑
function contentEdit(row) {
    //打开弹窗
    dialogFormVisible.value = true
    dialogType.value = 'edit'
    //把row里面的数据放到form里面去
    form.value = row
    //判断是新增还是编辑
}
</script>