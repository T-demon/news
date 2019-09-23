<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 00:25:42
 * @LastEditTime: 2019-09-23 16:56:23
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
  <div class="inputs">
    <AuthInput
     placeholder="输入手机号码"
      :value="form.username"
       @input="handleUsername"
       :rule="/^1[0-9]{4,10}$/"
        type="text"
        err_message="手机号码格式不正确"
       >
     </AuthInput>
       <AuthInput
        placeholder="输入密码"
        v-model="form.password"
        :rule="/^[0-9a-zA-Z]{3,12}$/"
        err_message="密码格式不正确"
        type="password"
        >
        </AuthInput>
        <p class="tips">
        没有账号？ 
        <router-link to="/register">去注册</router-link>
      </p>

 </div>
     

    <!-- 登录按钮 -->
    <AuthButton text="登录" @click="handleSubmit"></AuthButton>
  </div>
</template>





<script>
import AuthInput from "@/components/AuthInput";
import AuthButton from "@/components/AuthButton"


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
      this.$axios({
        url: "/login",
        method: "POST",  // method相当于type
        data: this.form
        // .then的回调函数相当于success
      }).then( res => {
        const {message} = res.data;

        if(message === "登录成功"){
          // 跳转到首页
          this.$router.push("/")
        }
      });
    }
    
  },

  components: {
    AuthInput,
    AuthButton
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

.inputs{
    input{
      margin-bottom: 20px;
    }
  }
   .tips{
    text-align: right;
    margin-bottom: 20px;
    a{
      color:#3385ff;
    }
  }
</style>