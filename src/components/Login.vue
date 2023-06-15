<template>
  <div class="login-container">
    <el-card class="login-card">
      <h2>登录页</h2>
      <el-form class="login-form" :model="form" label-position="top" @submit.native.prevent="login">
        <el-form-item label="用户名">
          <el-input v-model="form.username" placeholder="请输入用户名" clearable></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input v-model="form.password" type="password" placeholder="请输入密码" clearable></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" native-type="submit">登录</el-button>
        </el-form-item>
      </el-form>
      <div class="footer">
        <span>备案号：XXXXXX</span>
      </div>
    </el-card>
  </div>
</template>

<script lang="ts" setup>
import { ElInput, ElForm, ElFormItem, ElButton, ElCard } from "element-plus";

import { ref } from "vue";

const form = ref({
  username: '',
  password: ''
});

const login = () => {
  // 在这里处理登录逻辑，比如向服务器发送请求验证用户凭据
  // 可以使用 form.value.username 和 form.value.password 来获取用户名和密码
  // 在此示例中，只打印登录信息到控制台
  console.log('用户名:', form.value.username);
  console.log('密码:', form.value.password);
};
</script>

<style lang="scss" scoped>
  .login-container {
    width: 100vw;
    height: 100vh;
    display: flex;
    flex: 1;
    justify-content: flex-end;
    align-items: center;
    background-image: url('@/assets/img/backgroud.jpg');
    background-size: cover;
    background-position: center;
  }

  .login-card {
    width: 400px;
    padding: 20px;
  }

  .login-form {
    width: 100%;
    margin-bottom: 20px;
  }

  .footer {
    text-align: right;
    color: #999;
  }
</style>
