<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 00:25:42
 * @LastEditTime: 2019-09-22 20:34:17
 -->
<template>
  <div>
      <keep-alive include="index,search">
      <router-view></router-view>
      </keep-alive>

  </div>
</template>

<script>
export default {
    data(){
        return {
            
        }
    }
}
</script>                                                                                                                                                                                                                                       
 
<style>
  @import url("http://at.alicdn.com/t/font_1426139_h6vn3jbl5q.css");
  @import url("../node_modules/vant/lib/index.css");
 
  *{
      padding: 0;
      margin: 0;
  }
  a{
      color: inherit;
  }
  a:hover{
      text-decoration: none;
  }
  ul,li,ol{
      list-style: none;
  }
  i,em{
      font-style: normal
  }
  

</style>