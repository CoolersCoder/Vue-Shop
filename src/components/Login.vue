<template>
  <div class="login_container">
    <div class="login_box">
      <!-- icon -->
      <div class="avatar_box">
        <img src="../assets/logo.png" alt />
      </div>
      <!-- login form  -->
      <el-form :model="loginForm" class="login_form">
        <!-- login usernmae -->
        <el-form-item>
          <el-input v-model="loginForm.username" prefix-icon="el-icon-user"></el-input>
        </el-form-item>
        <!-- login psd -->
        <el-form-item>
          <el-input v-model="loginForm.password" type="password" prefix-icon="el-icon-lock"></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary">Login</el-button>
          <el-button type="info">Reset</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        username: '',
        pasword: ''
      }
    }
  }
}
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
