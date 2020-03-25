<template>
  <el-form ref="demoForm" :model="form" label-width="80px">
    <el-form-item label="姓名" prop="name">
      <el-input v-model="form.name" />
    </el-form-item>
    <el-form-item label="性别" prop="sex">
      <el-radio-group v-model="form.sex">
        <el-radio :label="1">男</el-radio>
        <el-radio :label="2">女</el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item label="身份" prop="identity">
      <el-select v-model="form.identity" placeholder="请选择身份">
        <el-option v-for="dti in identitys" :key="dti" :label="dti" :value="dti" />
      </el-select>
    </el-form-item>
    <el-form-item label="出生日期" prop="birthday">
      <el-col :span="11">
        <el-date-picker v-model="form.birthday" type="date" placeholder="选择日期" style="width: 100%;" format="yyyy 年 MM 月 dd 日" value-format="yyyy-MM-dd" />
      </el-col>
    </el-form-item>
    <el-form-item label="业余爱好" prop="hobbyArr">
      <el-checkbox-group v-model="hobbyArr">
        <el-checkbox v-for="h in hobbys" :key="h" :label="h">{{ h }}</el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="是否激活" prop="isActive">
      <el-switch v-model="form.isActive" :active-value="1" :inactive-value="0" />
    </el-form-item>
    <el-form-item label="自我介绍" prop="introduce">
      <el-input v-model="form.introduce" type="textarea" />
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  name: 'DemoAddEditForm',
  data() {
    return {
      hobbys: ['篮球', '羽毛球', '乒乓球', '游泳'],
      identitys: ['学生', '人大代表', '码农', '其他'],
      hobbyArr: [],
      form: {
        name: '',
        identity: '',
        birthday: '',
        hobby: '',
        sex: '',
        isActive: '',
        introduce: ''
      }
    }
  },
  props: {
    'formType': {
      type: String,
      require: true,
      validator: function(value) { // 验证函数
        // 这个值必须匹配下列字符串中的一个
        return ['add', 'edit'].includes(value)
      }
    },
    'formInitData': {
      type: Object
    }
  },
  mounted() {
    if (this.formType == 'edit') {
      this.form = Object.assign({}, this.formInitData)
      this.hobbyArr = this.formInitData.hobby.split(',')
    }
  },
  watch: {
    hobbyArr: function(newVal) {
      this.form.hobby = newVal.join(',')
    },
    formType: function(newVal) {
      if (newVal == 'add') {
        this.initForm()
      }
      if (newVal == 'edit') {
        this.form = Object.assign({}, this.formInitData)
        this.hobbyArr = this.formInitData.hobby.split(',')
      }
    },
    formInitData: function(newVal) {
      this.form = Object.assign({}, this.formInitData)
      this.hobbyArr = this.formInitData.hobby.split(',')
    }
  },
  methods: {
    initForm() {
      this.hobbyArr = []
      this.$refs.demoForm.resetFields()
    }
  }
}
</script>

<style scoped>

</style>
