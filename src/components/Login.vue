<template>
  <el-form ref="form" :model="form" label-width="80px" class="login-container">
    <el-form-item label="用户名">
      <el-input v-model="form.username"></el-input>
    </el-form-item>
    <el-form-item label="密码">
      <el-input type="password" v-model="form.password"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">登录</el-button>
      <el-button>重置</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          username: '',
          password: ''
        },
        websocket:null
      }
    },
    methods: {
      onSubmit() {
        if('WebSocket' in window){
          this.websocket = new WebSocket("ws://127.0.0.1:8083/websocket/"+document.cookie.substring(17));
        }

        this.websocket.onopen = function(){
          console.log("连接成功");
          this.$router.push('/HelloWorld')
        }


      }
    }
  }
</script>

<style>
  .login-container {
    -webkit-border-radius: 5px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    background-clip: padding-box;
    margin: 100px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }
</style>
