<template>
<div class="register">
  <el-form :model="UserForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
    <el-form-item label="用户名" prop="username">
      <el-input v-model="UserForm.username"></el-input>
    </el-form-item>
    <el-form-item label="密码" prop="password">
      <el-input v-model="UserForm.password"></el-input>
    </el-form-item>
    <el-form-item label="年龄" prop="age">
      <el-input v-model="UserForm.age"></el-input>
    </el-form-item>
    <el-form-item label="学院" prop="college">
      <el-input v-model="UserForm.college"></el-input>
    </el-form-item>
    <el-form-item label="联系电话" prop="phone">
      <el-input v-model="UserForm.phone"></el-input>
    </el-form-item>
    <el-form-item label="身份" prop="rid">
      <el-select v-model="UserForm.rid" >
        <el-option label="学生" value="1"></el-option>
        <el-option label="教师" value="2"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="性别" prop="gender">
      <el-radio-group v-model="UserForm.gender">
        <el-radio label="男" value="1"></el-radio>
        <el-radio label="女" value="0"></el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm('ruleForm')">注册</el-button>
      <el-button @click="resetForm('ruleForm')">重置</el-button>
    </el-form-item>
  </el-form>
</div>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      UserForm: {
        username: '',
        password: '',
        age: '',
        college: '',
        phone: '',
        rid: '',
        gender: '',

      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 10, message: '长度在 6 到 10 个字符', trigger: 'blur' }
        ],
        age: [
          { required: true, message: '请输入年龄', trigger: 'blur' },
          { min: 0, max: 3, message: '年龄在0~100', trigger: 'blur' }
        ],
        college: [
          { required: true, message: '请输入学院', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        phone: [
          { required: true, message: '请输入联系电话', trigger: 'blur' },
          { min: 11, max: 11, message: '请输入11位手机号', trigger: 'blur' }
        ],
        rid: [
          { required: true, message: '请输入身份', trigger: 'blur' },

        ],
        gender: [
          { required: true, message: '请输入性别', trigger: 'blur' },

        ]




      }
    };
  },
  methods: {
    submitForm(formName) {
      const _this=this
      this.$refs[formName].validate((valid) => {
        if (valid) {
          axios.post('http://localhost:8081/user/register',_this.UserForm).then(function (resp){
            if(!resp.data.success){
              alert(resp.data.message)
            }else {
              console.log(resp),
                  alert("成功")
            }
          })
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
}
</script>

<style scoped>

</style>