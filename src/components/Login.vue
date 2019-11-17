<template>
  <div class="login_container">
    <div class="login_box">
      <!-- icon -->
      <div class="avatar_box">
        <img src="../assets/logo.png" alt />
      </div>
      <!-- login form  -->
      <el-form ref="loginFormRef" :model="loginForm" :rules="loginFormRules" class="login_form">
        <!-- login usernmae -->
        <el-form-item prop="username">
          <el-input v-model="loginForm.username" prefix-icon="el-icon-user"></el-input>
        </el-form-item>
        <!-- login psd -->
        <el-form-item prop="password">
          <el-input v-model="loginForm.password" type="password" prefix-icon="el-icon-lock"></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary" @click="login">Login</el-button>
          <el-button type="info" @click="resetLoginForm">Reset</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginForm: {
        username: "admin",
        pasword: "123456"
      },
      loginFormRules: {
        username: [
          {
            required: true,
            message: "Please input user name",
            trigger: "blur"
          }
        ],
        password: [
          {
            required: true,
            message: "Please input password",
            trigger: "blur"
          }
        ]
      }
    };
  },

  methods: {
    resetLoginForm() {
      this.$refs.loginFormRef.resetFields();
    },
    login() {
      this.$refs.loginFormRef.validate(async valid => {
        if (!valid) return;
        const { data: res } = await this.$http.post("login", this.loginForm);
        if (res.meta.status !== 200) return this.$message.error('fail')
        this.$message.success('success')
        window.sessionStorage.setItem("token", res.data.token);
        this.$router.push('/home')
      });
    }
  }
};
</script>

<style lang="less" scoped>
.login_container {
  background-color: cadetblue;
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
  .avatar_box {
    height: 130px;
    width: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    position: absolute;
    left: 50%;
    // -50%, -50% 横向和纵向 size base on the .avatar_box
    //图标上移
    transform: translate(-50%, -50%);
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
    padding: 10px;
    box-shadow: 0 0 10px #ddd;
  }
}
.btns {
  display: flex;
  justify-content: flex-end;
}
.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  //How to use box-sizing, 帮助你自适应内容而不至于因为设置padding， 超出盒子大小。
  box-sizing: border-box;
}
</style>
