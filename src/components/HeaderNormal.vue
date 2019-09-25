<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-25 14:09:28
 * @LastEditTime: 2019-09-25 19:17:04
 -->
<template>
  <!-- 个人中心页板块的头部 -->
  <div class="header">
      <span class="iconfont iconjiantou2" @click="$router.back()"></span>
      <h4>{{title}}</h4>
      <span> > </span>
  </div>
</template>

<script>
export default {
    props: ['title']
}
</script>

<style scoped lang="less">
    .header{
        height:60 / 360 * 100vw;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        span{
            display: block;
            padding:0 10px;
        }
        span:last-child{
            opacity: 0;
        }
    }
</style> 