<template>
  <div class="login_container">
    <!-- 头像区 -->
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/logo.png" alt />
      </div>
      <!-- 登陆表单区 -->
      <el-form
        ref="loginFromRef"
        :model="userForm"
        :rules="loginFormRules"
        label-width="0px"
        class="login-form"
      >
        <!-- 用户名 -->
        <el-form-item prop="username">
          <el-input v-model="userForm.username">
            <i slot="prefix" class="el-input__icon el-icon-user-solid"></i>
          </el-input>
        </el-form-item>
        <!-- 密码 -->
        <el-form-item prop="password">
          <el-input type="password" v-model="userForm.password">
            <i slot="prefix" class="el-input__icon el-icon-lock"></i>
          </el-input>
        </el-form-item>
        <!-- 按钮 -->
        <el-form-item class="btns">
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info" @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      userForm: {
        username: 'admin',
        password: '123'
      },
      loginFormRules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' }
        ],
        password: [{ required: true, message: '请输入密码', trigger: 'blur' }]
      }
    }
  },
  methods: {
    resetLoginForm: function() {
      this.$refs.loginFromRef.resetFields()
    },
    login: function() {
      this.$refs.loginFromRef.validate(async valid => {
        if (valid) {
          this.$message.success('登录成功')
          const token = 'k123'
          //登录请求
          //const {data:res} = await this.$http.post("login",this.userForm);
          //1.将登录成功后的token，保存到客户端的 sessionStorage 中
          //  1.1 项目中除了登陆之外的其它API接口，必须在登陆之后才能访问
          //  1.2 token 只应在当前网站打开期间生效，所以将 token  保存在sessionStorage 中
          window.sessionStorage.setItem('token', token)
          // 2. 通过编程试导航跳转到后台主页，路由地址是 /home
          this.$router.push('/home')
        } else {
          this.$message.error('验证失败')
          return false
        }
      })
    }
  }
}
</script>
<style lang="less" scoped>
.login_container {
  background-color: #2b4b6b;
  height: 100%;
}
.login_box {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.avatar_box {
  width: 130px;
  height: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: #eee;
  }
}
.btns {
  display: flex;
  justify-content: flex-end;
}
.login-form {
  position: absolute;
  width: 100%;
  bottom: 0;
  padding: 0 20px;
  box-sizing: border-box;
}
</style>