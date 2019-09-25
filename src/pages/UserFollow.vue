<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-25 19:12:35
 * @LastEditTime: 2019-09-25 19:52:59
 -->
<template>
  <div>
    <HeaderNormal title="我的关注"></HeaderNormal>
    <div class="item" v-for="(item,index) in list" :key="index">
      <div class="headimg">
        <img :src="$axios.defaults.baseURL + item.head_img" />
      </div>
      <div class="item-center">
        <p>{{item.nickname}}</p>
        <span>2019-09-25</span>
      </div>
      <span class="follow" @click="handelCancel(index)">取消关注</span>
    </div>
  </div>
</template>

<script>
import HeaderNormal from "@/components/HeaderNormal";
export default {
  components: {
    HeaderNormal
  },
  data(){
    return{
      list:[]
    }
  },
  mounted() {
    this.$axios({
      url: "/user_follows",
      headers: {
        Authorization: localStorage.getItem("token")
      }
    }).then(res => {
      const { data } = res.data;
      console.log(res)
      // 赋值给关注的列表
      this.list = data;
    });
  },
  methods:{
    handelCancel:function(index){
      const id = this.list[index].id
       this.$axios({
      url: "/user_unfollow/"+id,
      headers: {
        Authorization: localStorage.getItem("token")
      }
    }).then(res => {
      const {message} = res.data
      if(message === "取消关注成功"){
        this.list.splice(index,1);
        this.$toast.success(message);
      }
      
    });
    }
  }
};
</script>

<style lang="less" scoped>
.item {
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .item-center {
    flex: 1;
    padding-left: 10px;
  }
  .headimg {
    border-radius: 50%;
    background-color: #e5e5e5;
    img {
      width: 40/360 * 100vw;
      height: 40/360 * 100vw;
    }
  }
  .follow {
    display: block;
    background: #e5e5e5;
    padding: 0 10px;
    height: 26px;
    line-height: 26px;
    font-size: 12px;
    border-radius: 50px;
  }
}
</style>
