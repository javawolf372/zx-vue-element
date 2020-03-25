<template>
  <el-form :inline="true" :model="formInline" class="demo-form-inline">
    <el-form-item label="姓名">
      <el-input v-model="formInline.name" clearable placeholder="姓名" />
    </el-form-item>
    <el-form-item label="激活状态">
      <el-select v-model="formInline.isActive" placeholder="激活状态" clearable>
        <el-option label="未激活" value="0" />
        <el-option label="已激活" value="1" />
      </el-select>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="toQuery">查询</el-button>
      <el-button v-has="20280102" type="primary" icon="el-icon-plus" @click="toAdd">添加</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  name: 'Query',
  data() {
    return {
      formInline: {
        name: '',
        isActive: ''
      }
    }
  },
  methods: {
    toQuery() {
      this.$emit('toQuery', this.formInline)
    },
    toAdd() {
      this.$emit('toAdd')
    }
  }
}
</script>

<style scoped>

</style>
