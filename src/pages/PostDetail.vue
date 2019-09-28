<template>
  <div class="container">
    <div class="detail">
      <div class="detail-header">
        <span class="iconfont iconjiantou2" @click="$router.back()"></span>
        <i class="iconfont iconnew"></i>
        <span class="focus" v-if="!detail.has_follow" @click="handleFollow">关注</span>
        <span class="focus focus_active" v-else @click="handleUnfollow">已关注</span>
      </div>
      <h3 class="title">{{detail.title}}</h3>
      <div class="detail-info">
        <span>{{detail.user.nickname}}</span>
        <span>2019-10-10</span>
      </div>
      <div class="detail-content" v-html="detail.content" v-if="detail.type ===1 "></div>

      <!-- 视频详情的内容 -->
      <div class="video-wrap" v-if="detail.type === 2">
        <video
          src="https://video.pearvideo.com/mp4/adshort/20190927/cont-1607446-14434032_adpkg-ad_hd.mp4"
          class="video"
        ></video>

        <div class="video-info">
          <div class="video-user">
            <img :src="$axios.defaults.baseURL + detail.user.head_img" />
            <span>{{detail.user.nickname}}</span>
          </div>

          <span class="focus" v-if="!detail.has_follow" @click="handleFollow">关注</span>
          <span class="focus focus_active" v-else @click="handleUnfollow">已关注</span>
        </div>
      </div>

      <!-- 点赞 -->
      <div class="post-btns">
        <span @click="handleLike" :class="{ like_active: detail.has_like }
        ">
          <i class="iconfont icondianzan"></i>
          {{detail.like_length}}
        </span>
        <span>
          <i class="iconfont iconweixin"></i>
          微信
        </span>
      </div>
    </div>
    <PostFooter :post="detail" @handleStar="handleStar"></PostFooter>
  </div>
</template>

<script>
import PostFooter from "@/components/PostFooter";
export default {
  components: {
    PostFooter
  },
  data() {
    return {
      detail: {
        user: {}
      }
    };
  },
  mounted() {
    const { id } = this.$route.params;
    const token = localStorage.getItem("token");
    const config = {
      url: "/post/" + id
    };
    if (token) {
      config.headers = {
        Authorization: token
      };
    }

    this.$axios(config).then(res => {
      const { data } = res.data;
      this.detail = data;
    });
  },
  methods: {
    handleFollow() {
      console.log(123);
      this.$axios({
        url: "/user_follows/" + this.detail.user.id,
        headers: {
          Authorization: localStorage.getItem("token")
        }
      }).then(res => {
        const { message } = res.data;
        console.log(res);
        if (message === "关注成功") {
          this.detail.has_follow = true;
          this.$toast.success(message);
        }
      });
    },
    handleUnfollow() {
      this.$axios({
        url: "/user_unfollow/" + this.detail.user.id,

        headers: {
          Authorization: localStorage.getItem("token")
        }
      }).then(res => {
        const { message } = res.data;

        if (message === "取消关注成功") {
          this.detail.has_follow = false;
          this.$toast.success(message);
        }
      });
    },
    handleStar() {
      this.$axios({
        url: "/post_star/" + this.detail.id,
        headers: {
          Authorization: localStorage.getItem("token")
        }
      }).then(res => {
        const { message } = res.data;

        if (message === "收藏成功") {
          this.detail.has_star = true;
        }

        if (message === "取消成功") {
          this.detail.has_star = false;
        }

        this.$toast.success(message);
      });
    },
    handleLike() {
      this.$axios({
        url: "/post_like/" + this.detail.id,
        headers: {
          Authorization: localStorage.getItem("token")
        }
      }).then(res => {
        const { message } = res.data;

        if (message === "点赞成功") {
          this.detail.has_like = true;
          this.detail.like_length++;
        }

        if (message === "取消成功") {
          this.detail.has_like = false;
          this.detail.like_length--;
        }

        this.$toast.success(message);
      });
    },

  }
};
</script>

<style lang="less" scoped>
.container {
  padding-bottom: 100 / 360 * 100vw;
  padding: 0px 15px 100 / 360 * 100vw;
}
.detail {
  border-bottom: 3px solid #999;
  padding-bottom: 20px;
  .detail-header {
    height: 60/360 * 100vw;
    // position: fixed;
    background-color: #fff;
    display: flex;
    width: 100%;
    box-sizing: border-box;
    justify-content: space-between;
    align-items: center;
    i {
      flex: 1;
      font-size: 55/360 * 100vw;
    }
    title {
      display: block;
      margin-top: 60px;
    }
    .focus {
      display: block;
      padding: 5px 20px;
      background-color: #ff0000;
      font-size: 12px;
      box-sizing: border-box;
      color: #fff;
      border-radius: 50px;
    }
    .focus_active {
      border: 1px #ccc solid;
      color: #333;
      background: none;
    }
  }
  .detail-info {
    font-size: 12px;
    color: #999;
    padding: 10px;
  }
  .detail-content {
    margin-top: 10px;
    font-size: 14px;
    line-height: 1.5;
    /deep/ img {
      max-width: 100%;
    }
  }

  .video {
    width: 100%;
  }

  .video-info {
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .video-user {
      display: flex;
      align-items: center;
      font-size: 12px;
      color: #999;
    }

    img {
      width: 18px;
      height: 18px;
      border-radius: 50%;
      margin-right: 10px;
    }
  }
  .post-btns {
    margin-top: 30px;
    display: flex;
    justify-content: space-around;
    span {
      padding: 0 15px;
      height: 30 / 360 * 100vw;
      line-height: 30 / 360 * 100vw;
      font-size: 12px;
      border: 1px #ddd solid;
      border-radius: 50px;
    }
    .iconweixin {
      color: #07c907;
    }
    .like_active {
      color: red;
    }
  }
}
</style>