<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 00:25:42
 * @LastEditTime: 2019-09-24 16:11:31
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
    <!--提取动态元素 v-model中等同于value和@input 在输入时触发 错误提示也是动态值 要进行校验所有需要传规则 -->
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
    // 触发input事件 将输入框中的值存到该组件中
    handleUsername(value){
      this.form.username=value;
    },
    handleSubmit(){
      // 拿到数据后发送axios请求
      console.log(this.form)
      this.$axios({
        url: "/login",
        method: "POST",  // method相当于type
        data: this.form
        // .then的回调函数相当于success
      }).then( res => {
        console.log(res)
        // 解构出来 
        const {message,data} = res.data;
        // 如果登录成功 将token值和用户id存储的本地
        // 用户登录成功之后,在后端(服务器端)会根据用户信息生成一个唯一的值.这个值就是 token
        if(message === "登录成功"){
          localStorage.setItem('token',data.token)
          localStorage.setItem('user_id',data.user.id)

          // 跳转到个人中心
          this.$router.push("/Personal")
        }
      });
    }
    
  },

  components: {
    AuthInput,
    AuthButton
  }
}

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