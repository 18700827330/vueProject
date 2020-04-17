<template>
  <div class="login-contanier">
    <div class="login-box">
      <!-- 头像区域 -->
      <div class="avatar-box">
        <img src="../assets/logo.png" alt="图标" />
      </div>
      <!-- 表单区域 -->
      <el-form
        ref="loginFromRef"
        :model="loginFrom"
        label-width="80px"
        class="login-from"
        :rules="loginFromRules"
      >
        <el-form-item label="用户名" prop="username">
          <el-input prefix-icon="el-icon-search" v-model="loginFrom.username"></el-input>
        </el-form-item>
        <!-- 密码区域 -->
        <el-form-item label="密码" prop="password">
          <el-input prefix-icon="el-icon-search" v-model="loginFrom.password" type="password"></el-input>
        </el-form-item>
        <!-- 按钮区域 -->
        <el-form-item class="btns">
          <el-button type="primary" @click="registerLoginForm">登录</el-button>
          <el-button type="info" @click="resetLoginForm">注册</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      loginFrom: {
        username: '',
        password: 'dddd'
      },
      loginFromRules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 6, max: 12, message: '长度在 6 到 12 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 12, message: '长度在 6 到 10 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm () {
      console.log(this)
      this.$refs.loginFromRef.resetFields()
    },
    registerLoginForm() {
      console.log(this)
      this.$refs.loginFromRef.validate(async valid => {
        console.log(valid)
        if (!valid) {
          const result = await this.$http.post('login', this.loginFrom)
          console.log(result)
        }
      })
    }
  }
}
</script>
<style lang="less" scoped>
.login-contanier {
  height: 100%;
  background-color: #2b4b6b;
}
.login-box {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  .avatar-box {
    width: 130px;
    height: 130px;
    border: 1px solid #ccc;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0px 0px 10px #ddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%, -36%);
    background-color: #2b4b6b;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
  }
}
.login-from {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
.btns {
  display: flex;
  justify-content: flex-end;
}
</style>
