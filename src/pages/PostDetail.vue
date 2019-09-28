<template>
  <div class="container">
    <div class="detail">
      <div class="detail-header">
        <span class="iconfont iconjiantou2" @click="$router.back()"></span>
        <i class="iconfont iconnew"></i>
        <span class="gzbtn">关注</span>
      </div>
      <h3 class="title">{{detail.title}}</h3>
      <div class="detail-info">
        <span>{{detail.user.nickname}}</span>
        <span>2019-10-10</span>
      </div>
      <div class="detail-content" v-html="detail.content"></div>
      <div class="post-btns">
        <span>
          <i class="iconfont icondianzan"></i>
          {{detail.like_length}}666
        </span>
        <span>
          <i class="iconfont iconweixin"></i>
          微信
        </span>
      </div>
    </div>
    <PostFooter></PostFooter>
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
    this.$axios({
      url: "/post/" + id,
      methed: "GET"
    }).then(res => {
      const { data } = res.data;
      this.detail = data;
      console.log(this.detail);
    });
  }
};
</script>

<style lang="less" scoped>
.container {
  padding-bottom: 100 / 360 * 100vw;
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
    .gzbtn {
      display: block;
      padding: 5px 20px;
      background-color: #ff0000;
      font-size: 12px;
      box-sizing: border-box;
      color: #fff;
      border-radius: 50px;
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
  }
}
</style>