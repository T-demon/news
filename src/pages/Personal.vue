<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-24 14:07:45
 * @LastEditTime: 2019-09-25 19:15:08
 -->
<template>
  <div>
    <router-link to="/Edit">
      <div class="profile">
        <img :src="profile.head_img" alt />
        <div class="profile-center">
          <div class="name">
            <span class="iconfont iconxingbienan" @click="this.$router.back()"></span>
            {{profile.nickname}}
          </div>
          <div class="time">2019-10-1</div>
        </div>
        <i class="iconfont iconjiantou1"></i>
      </div>
    </router-link>
    <router-link to="/UserFollow">
        <CellBar label="我的关注" text="关注的用户"></CellBar>
    </router-link>
    <router-link to="/UserComment">
        <CellBar label="我的跟帖" text="跟帖/回复"></CellBar>
    </router-link>
    
    <CellBar label="我的关注" text="文章/视频"></CellBar>
    <CellBar label="退出" @click="handelLoginout"></CellBar>
  </div>
</template>

<script>
import CellBar from "@/components/CellBar";

export default {
  components: {
    CellBar
  },
  data() {
    return {
      profile: {}
    };
  },
  mounted() {
    // 页面加载时触发 发送axios请求
    this.$axios({
      url: "/user/" + localStorage.getItem("user_id"),
      //  将服务器返回给本地的token值 加入请求头中
      headers: {
        Authorization: localStorage.getItem("token")
      }
    }).then(res => {
      const { data } = res.data;
      console.log(res);
      this.profile = data;
      // 设置默认头现象
      if (data.head_img) {
        this.profile.head_img =
          this.$axios.defaults.baseURL + this.profile.head_img;
      } else {
        this.profile.head_img = "./static/男头像.png";
      }
    });
  },
  methods: {
    // 退出时将存在本地的token和用户id进行移除
    handelLoginout: function() {
      localStorage.removeItem("token");
      localStorage.removeItem("user_id");

      this.$router.replace("/");
    }
  }
};
</script>

<style lang="less" scoped>
.profile {
  display: flex;
  padding: 20px;
  border-bottom: 2px solid #b8b8b8;
  justify-content: space-around;
  align-items: center;
  img {
    width: 70 / 360 * 100vw;
    height: 70 / 360 * 100vw;
    border-radius: 50%;
  }
  .profile-center {
    flex: 1;
    margin-left: 10px;
    span {
      color: skyblue;
    }
    .time {
      color: #b8b8b8;
      font-size: 14px;
    }
  }
}
</style>
