<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 00:25:42
 * @LastEditTime: 2019-09-22 19:17:56
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

    <AuthInput
     placeholder="输入手机号码"
      :value="form.username"
       @input="handleUsername"
       :rule="/^1[0-9]{6,10}$/"
        err_message="手机号码格式不正确"
       >
     </AuthInput>

       <AuthInput
        placeholder="输入密码"
        v-model="form.password"
        :rule="/^[0-9a-zA-Z]{3,12}$/"
        err_message="密码格式不正确"
        >
        </AuthInput>

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