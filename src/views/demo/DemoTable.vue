<template>
  <div>
    <el-table
      :data="tableData"
      :stripe="true"
      :border="true"
      :highlight-current-row="true"
      style="width: 100%"
    >
      <el-table-column label="姓名" min-width="15%">
        <template slot-scope="scope">
          <el-popover trigger="hover" placement="top">
            <p>姓名: {{ scope.row.name }}</p>
            <p>爱好: {{ scope.row.hobby }}</p>
            <div slot="reference" class="name-wrapper">
              <el-tag size="medium">{{ scope.row.name }}</el-tag>
            </div>
          </el-popover>
        </template>
      </el-table-column>
      <el-table-column label="性别" min-width="10%">
        <template slot-scope="scope">
          <span style="margin-left: 10px">{{ scope.row.sex==1?'男':'女' }}</span>
        </template>
      </el-table-column>
      <el-table-column label="身份" min-width="10%">
        <template slot-scope="scope">
          <span style="margin-left: 10px">{{ scope.row.identity }}</span>
        </template>
      </el-table-column>
      <el-table-column label="出生日期" min-width="15%">
        <template slot-scope="scope">
          <span>{{ new Date(scope.row.birthday).toLocaleString().split(' ')[0] }}</span>
        </template>
      </el-table-column>
      <el-table-column label="爱好" min-width="20%">
        <template slot-scope="scope">
          {{ scope.row.hobby }}
        </template>
      </el-table-column>
      <el-table-column label="个人介绍" min-width="25%">
        <template slot-scope="scope">
          {{ scope.row.introduce }}
        </template>
      </el-table-column>
      <el-table-column label="是否激活" min-width="10%">
        <template slot-scope="scope">
          <el-switch :value="scope.row.isActive==1" active-color="#13ce66" inactive-color="#ff4949" />
        </template>
      </el-table-column>
      <el-table-column label="操作" min-width="20%">
        <template slot-scope="scope">
          <el-button
            v-has="20280103"
            round
            type="primary"
            size="mini"
            @click="toEdit(scope.$index, scope.row)"
          >编辑</el-button>
          <el-popconfirm
            title="确定删除该条记录吗？"
            style="margin-left: 10px"
            @onConfirm="deleteConfirm(scope.row.id)"
          >
            <el-button slot="reference" v-has="20280104" round size="mini" type="danger">删除</el-button>
          </el-popconfirm>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      style="text-align: center;margin-top: 5px"
      background
      layout="sizes, prev, pager, next, ->, total"
      prev-text="上一页"
      next-text="下一页"
      :page-size="pageSize"
      :current-page="currentPage"
      :total="totalSize"
      @size-change="changeSize"
      @current-change="changeCurrPage"
    >
    </el-pagination>
  </div>
</template>

<script>
export default {
  name: 'Table',
  data() {
    return {
      tableData: [],
      currentPage: 1,
      pageSize: 10,
      totalSize: 0,
      formInline: {}
    }
  },
  mounted() {
    this.initData(this.formInline)
  },
  methods: {
    initData() {
      const param = Object.assign({
        size: this.pageSize,
        currPage: this.currentPage
      }, this.formInline)
      this.$store.dispatch('demo/list', param)
        .then((response) => {
          this.tableData = response.data.list
          this.totalSize = response.data.total
        })
        .catch((error) => {
          console.log('初始化demo列表错误：' + error)
        })
    },
    query(formInline) {
      this.formInline = formInline
      this.initData()
    },
    changeSize(size) {
      this.pageSize = size
      this.initData()
    },
    changeCurrPage(currPage) {
      this.currentPage = currPage
      this.initData()
    },
    deleteConfirm(id) {
      this.$store.dispatch('demo/del', id)
        .then((response) => {
          this.initData()
          this.$message.success('操作成功!')
        })
        .catch((error) => {
          this.$message.error('操作失败：' + error)
        })
    },
    toEdit(index, rowData) {
      this.$emit('toEdit', rowData)
    }
  }
}
</script>

<style scoped>

</style>
