<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 00:25:42
 * @LastEditTime: 2019-09-22 14:50:04
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
    <div>
      <input type="text" />
    </div>
    <div>
      <input type="text" />
    </div>

    <!-- 登录按钮 -->
    <button>登录</button>
  </div>
</template>

<script>
// var AuthInput = import from ""
export default {};
</script>

<style lang="less" scoped>

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