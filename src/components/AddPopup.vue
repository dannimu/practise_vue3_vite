<template>
    <el-button @click="dialogFormVisible = true" type="primary">增加</el-button>
    <el-dialog v-model="dialogFormVisible" :title="dialogType==='add'?'新增':'编辑'">
        <el-form :model="form">
            <el-form-item label="姓名" :label-width="formLabelWidth">
                <el-input v-model="form.name" autocomplete="off" />
            </el-form-item>
            <el-form-item label="邮箱" :label-width="formLabelWidth">
                <el-input v-model="form.email" autocomplete="off" />
            </el-form-item>
            <el-form-item label="电话" :label-width="formLabelWidth">
                <el-input v-model="form.phone" autocomplete="off" />
            </el-form-item>
            <el-form-item label="Zones" :label-width="formLabelWidth">
                <el-select v-model="form.region" placeholder="Please select a zone">
                    <el-option label="Zone No.1" value="shanghai" />
                    <el-option label="Zone No.2" value="beijing" />
                </el-select>
            </el-form-item>
        </el-form> 
        <template #footer>
            <span class="dialog-footer">
                <el-button type="primary" @click="dialogForm">确认</el-button>
            </span>
        </template>
    </el-dialog>
</template>
<script>
import {ref,reactive} from 'vue'
export default {
    setup(props,context) {
        const dialogFormVisible = ref(false)
        const formLabelWidth = ref('140px')
        const dialogType = ref('add')
        const form = reactive({})
        function dialogForm() {
            dialogFormVisible.value = ref(false)
            context.emit('dialogForm',form)
        }

        return{
            dialogFormVisible,formLabelWidth,form,dialogType,dialogForm
        }
    }
}
</script>