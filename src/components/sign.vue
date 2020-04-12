<template>
  <div class="sign">
    <div class="sign-wrapper">
      <input type="file" name="image" accept="image/*" @change="onchangeImg" class="touxiang"/>
        <img alt="" :src="imgStr" class="headimg"/>
        <p class="change">修改头像</p>
        <p class="error">{{errorStr}}</p>
      <el-form ref="form" :model="form">
        <el-form-item label="昵称" prop="username" class="sign-user">
          <el-input v-model="form.username" placeholder="昵称" class="sign-input"></el-input>
        </el-form-item>
        <el-form-item label="输入密码" prop="password" class="login-user">
           <el-input v-model="form.password" placeholder="密码" class="sign-input"></el-input>
        </el-form-item>
        <el-form-item label="确认密码" prop="checkpass" class="login-user">
          <el-input v-model="form.checkpass" placeholder="确认密码" class="sign-input"></el-input>
        </el-form-item>
        <el-form-item class="sign-button">
          <el-button size="large" class="form-submit" @click="sign(form)">注册</el-button>
          <p class="login" @click="gotoLogin()">已有账号？立即登录</p>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'sign',
  data() {
    let validatePass = (rule,value,callback) => {
      if (value === ""){
        callback(new Error("请输入密码"));
      }else {
        if (this.form.checkpass !==""){
          this.$refs.form.validateField("checkpass");
        }
        callback();
      }
    };
    let validatePass2 = (rule,value,callback) => {
      if (value === ""){
        callback(new Error("请再次输入密码"));
      } else if (value !== this.form.password) {
        callback(new Error("两次输入密码不一致"));
      }else {
        callback();
      }
    };
    return {
      form: {
        username: '',
        password: '',
        checkpass: ''
      },
      rules: {
        username: [{required: true,message: '请输入昵称',trigger: 'blur'}],
        password: [{validator: validatePass, trigger: 'blur'}],
        checkpass: [{validator: validatePass2, trigger:'blur'}]
      },
      imgStr: require('../assets/logo.png'),
      errorStr: ''
    }
  },
  methods: {
    onchangeImg(e){
      var file=e.target.files[0];
      let imgSize = file.size;
      console.log(imgSize);
      var _this = this;
      if (imgSize <= 50 * 1024){
        _this.errorStr = '';
        var reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onloadend = function () {
          var dataURL = reader.result
          console.log(dataURL)
          _this.imgStr = dataURL
        }
      }else{
        console.log('大小不合适')
        _this.errorStr = '图片大小超出范围'
        }
    },
    sign (formname) {
      this.$ref[formname].validate(valid => {
        if (valid) {
          setTimeout(() => {
            alert('注册成功');
          },400);
        }else {
          alert("注册失败");
          return false;
        }
      })
    },
    gotoLogin() {
      this.$router.push({
        path: '/log'
      })
    }
  } 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .sign-wrapper{
    position: relative;
    height: 800px;
    width: 500px;
    margin: 0 auto;
    border: 5px  solid lightblue;
  }
  .sign-wrapper .headimg{
    height: 50px;
    width: 50px;
    border-radius: 50%;
    border: 1px solid bisque;
    margin: 0 auto;
  }
</style>
