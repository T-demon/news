<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-24 14:07:45
 * @LastEditTime: 2019-09-24 15:00:59
 -->
<template>
  <div>
      <div class="profile">
          <img src="../../static/男头像.png">
          <div class="profile-center">
              <div class="name">
                    <span class="iconfont iconxingbienan"></span>
                    火星网友
              </div>
              <div class="time">
                  2019-10-1
              </div>
          </div>
          <i class="iconfont iconjiantou1"></i>

      </div>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="less" scoped>
    .profile{
        display: flex;
        padding: 20px;
        border-bottom:2px solid #b8b8b8;
        justify-content: space-around;
        align-items: center;
       img{
            width: 70 / 360 * 100vw;
            height: 70 / 360 * 100vw;
            border-radius: 50%;
       }
       .profile-center{
           flex: 1;
           margin-left: 10px;
           span{
               color: skyblue;
           }
           .time{
               color: #b8b8b8;
               font-size: 14px;
           }
       }
       
    }
</style>>

</style>