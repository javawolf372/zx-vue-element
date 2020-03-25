<template>
  <div>
    <demo-query @toQuery="toQuery" @toAdd="toAdd"></demo-query>
    <demo-table ref="demoTable" @toEdit="toEdit"></demo-table>
    <el-dialog title="个人信息" :visible.sync="dialogFormVisible">
      <demo-add-edit-form ref="demoAddEditForm" :form-type="addOrEdit" :form-init-data="editData"></demo-add-edit-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import DemoQuery from './DemoQuery'
import DemoTable from './DemoTable'
import DemoAddEditForm from './DemoAddEditDialog'

export default {
  name: 'Index',
  components: { DemoAddEditForm, DemoTable, DemoQuery },
  data() {
    return {
      formLabelWidth: '100px',
      dialogFormVisible: false,
      addOrEdit: '',
      editData: {}
    }
  },
  methods: {
    toQuery(queryData) {
      this.$refs.demoTable.query(queryData)
    },
    submit() {
      this.$store.dispatch('demo/' + this.addOrEdit, this.$refs.demoAddEditForm.form)
        .then((response) => {
          this.dialogFormVisible = false
          this.$refs.demoTable.initData()
          this.$message.success('操作成功!')
        })
        .catch((error) => {
          this.$message.error('操作失败：' + error)
        })
    },
    toAdd() {
      this.dialogFormVisible = true
      this.addOrEdit = 'add'
    },
    toEdit(rowData) {
      this.dialogFormVisible = true
      this.addOrEdit = 'edit'
      this.editData = rowData
    }
  }
}
</script>

<style scoped>

</style>
