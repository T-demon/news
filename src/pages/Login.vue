<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 00:25:42
 * @LastEditTime: 2019-09-22 17:13:23
 -->
<template>
  <div class="login">
    <div class="close">
      <span class="iconfont iconicon-test"></span>
    </div>

    <div class="logo">
      <span class="iconfont iconnew"></span>
    </div>
    <!-- 输入框 -->

    <AuthInput placeholder="手机号码" :value="form.username" @input="handleUsername"></AuthInput>

    <!-- 登录按钮 -->
    <button @click="handleSubmit">登录按钮</button>
  </div>
</template>





<script>
import AuthInput from "@/components/AuthInput";

export default {
  data() {
    return {
      form: {
        username: "",
        password: ""
      }
    };
  },
  methods: {
    handleUsername(value){
      this.form.username=value;
    },
    handleSubmit(){
      console.log(this.form)
    }
    
  },

  components: {
    AuthInput
  }
};
</script>




<style lang="less" scoped>
.login {
  padding: 20px;
}
.close {
  padding: 20px;
  span {
    font-size: 27/360 * 100vw;
  }
}

.logo {
  display: flex;
  justify-content: center;
  span {
    display: block;
    font-size: 126/360 * 100vw;
    color: #d81e06;
  }
}
</style>