<template>
  <div class="log">
    <div class="log-wrapper" @keyup.enter="login">
      <el-form ref="formLogin" :model="form" label-width="0">
        <el-form-item label="昵称" prop="username" class="login-user">
          <el-input v-model="formLogin.username" placeholder="昵称" class="log-input"></el-input>
        </el-form-item>
        <el-form-item label="输入密码" prop="password" class="login-user">
           <el-input v-model="formLogin.password" placeholder="密码" class="log-input"></el-input>
        </el-form-item>
        <el-form-item class="log-button">
          <el-button size="large" class="log-in" @click="login()">登录</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'log',
  data () {
    return {
      formLogin:{
        username: '',
        password: ''
      },
      rules: {
        username: [{required: true,message: '请输入昵称',trigger: 'blur'}],
        password: [{required:true, trigger: 'blur'}]
      }
    }
  },
  methods: {
    login(){
      this.$refs.formLogin.validate((valid) => {
        if (valid) {
          this.$router.push({path: '/chat'})
        }
      })
    }
  }
}
</script>

<style>

</style>