<template>
  <div>
    <div class="header">
      <div class="logo">
        <span class="iconfont iconnew"></span>
      </div>
      <div class="serach">
        <i class="iconfont iconsearch"></i>
        <span>搜索新闻</span>
      </div>
      <router-link to="/Personal">
        <span class="iconfont iconwode user"></span>
      </router-link>
    </div>

    <div>
      <van-tabs v-model="active" swipeable>
        <van-tab v-for="(item,index) in categores" :title="item.name" :key="index">内容{{index}}</van-tab>
      </van-tabs>
    </div>

    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>
</template>

<script>
export default {
    data(){
        return{
         active:localStorage.getItem("token") ? 1 : 0, 
         categores:[]
        }
    },
  mounted() {

        const config = {
            url: "/category",
        }
        if(localStorage.getItem("token")){
            config.headers = {
                 Authorization: localStorage.getItem("token")
            }
        }
    this.$axios(config).then(res=>{
        console.log(res);
        const{data} = res.data
        this.categores=data
        
    });
  }
};
</script>

<style scoped lang="less">
.header {
  height: 50/360 * 100vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ff0000;
  .logo {
    color: #fff;
    span {
      font-size: 48/360 * 100vw;
    }
  }
  .serach {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 35/360 * 100vw;
    background: rgba(255, 255, 255, 0.5);
    margin: 10px 20px;
    color: #fff;
    border-radius: 50px;
    span {
      padding-left: 5px;
    }
  }
  .user {
    font-size: 28/360 * 100vw;
    padding: 0 10px;
    color: #fff;
  }
}
</style>