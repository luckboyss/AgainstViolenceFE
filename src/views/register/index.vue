<template>
  <div class="register-container">
    <el-form
      ref="registerForm"
      size="mini"
      label-width="80px"
      label-position="left"
      :rules="rules">
      <div class="title-container">
        <h3 class="title">注册</h3>
      </div>
      <el-form-item label="用户名" prop="username">
        <el-input
          v-model="registerForm['username']"
          placeholder="请输入正确邮箱地址"
          name="username"
          tabindex="1"
          auto-complete="false"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input
          ref="password"
          v-model="registerForm['password']"
          placeholder="请输入密码"
          tabindex="2"
          :key="passwordType"
          :type="passwordType"></el-input>
      </el-form-item>
      <el-form-item label="确认密码" prop="rePassword">
        <el-input v-model="registerForm['rePassword']"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button>注册</el-button>
      </el-form-item>
      <el-form-item>
        <el-row justify="end">
          <el-col :span="Number(24)">
            <router-link to="/login">使用已有账号登录</router-link>
          </el-col>
        </el-row>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
  import { validUsername } from '@/utils/validate'

  export default {
    name: 'register',
    data() {
      const vaildateRePassword = (rules, value, callback) => {
        let password = this.registerForm['password'], repassword = this.registerForm['rePassword']
        if (password !== repassword) {
          callback(new Error('密码不相等'))
        } else {
          callback()
        }
      }
      const vaildatePassword = (rrules, value, callback) => {
        if (value.length < 6) {
          callback(new Error('密码不能少于6位'))
        } else {
          callback()
        }
      }
      return {
        registerForm: {
          username: '',
          password: '',
          rePassword: ''
        },
        rules: {
          username: [
            { required: true, message: '请填写注册邮箱', trigger: 'blur' },
            { type: 'email', message: '请填写正确的邮箱格式', trigger: ['blur', 'change'] }
          ],
          password: [
            { required: true, trigger: 'blur', validator: vaildatePassword }
            ],
          rePassword: [{ required: true, trigger: ['blur', 'change'], validator: vaildateRePassword }]
        },
        passwordType: 'password'
      }
    }
  }
</script>

<style scoped>

</style>
