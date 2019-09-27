<template>
  <div>
    <!-- 单张图显示 -->
    <div class="post" v-if="posts.cover.length>0 && posts.cover.length<3 && posts.type === 1">
      <div class="card-left">
        <div class="post-title">{{posts.title}}</div>
        <div class="post-info">
          <span>{{posts.user.nickname}}</span>
          <span>跟贴:{{posts.comment_length}}</span>
        </div>
      </div>
      <div class="card-img">
        <img :src="posts.cover[0].url" />
      </div>
    </div>
    <!-- 多张图显示 -->
    <div class="img-cart" v-if="posts.cover.length >= 3">
      <div class="post-title">{{posts.title}}</div>
      <div class="img-list">
        <img v-for="(item, index) in posts.cover" :key="index" :src="item.url" v-if="index < 3" />
      </div>
      <p class="post-info">
        <span>{{posts.user.nickname}}</span>
        <span>{{posts.comment_length}}跟帖</span>
      </p>
    </div>
    <!-- 视频显示 -->
    <div class="video-cart" v-if="posts.type ===2 && posts.cover.length ===1">
      <div class="post-title">{{posts.title}}</div>

      <div class="video">
        <img :src="posts.cover[0].url" />
      </div>

      <span class="video-layer">
        <i class="iconfont iconshipin"></i>
      </span>

      <div class="post-info">
        <span>{{posts.user.nickname}}</span>
        <span>跟贴:{{posts.comment_length}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["posts"],
  mounted() {
    // console.log(this.posts);
  }
};
</script>

<style lang="less" scoped>
.post {
  padding: 10px;
  display: flex;
  justify-content: center;
  height: 80/360 * 100vw;
  border-bottom: 1px solid #eee;
  .card-left {
    display: flex;
    padding-top: 10px;
    flex-direction: column;
    justify-content: space-between;
    height: 80/ 360 * 100vw;
    flex: 1;
    .post-title {
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
    }
    .post-info {
      font-size: 12px;
      color: #999;
    }
  }
  .card-img {
    img {
      height: 80/360 * 100vw;
      width: 120/360 * 100vw;
      padding-left: 10px;
      object-fit: cover;
    }
  }
}

.img-cart {
  padding: 10px;
  border-bottom: 1px solid #eee;
  .img-list {
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
    img {
      margin-bottom: 10px;
      display: block;
      width: 33%;
      height: 80 / 360 * 100vw;
      object-fit: cover;
    }
  }
  .post-info {
    font-size: 12px;
    color: #999;
  }
}
.video-cart {
  padding: 20px 10px;
  position: relative;
  .post-title {
    font-size: 14px;
    line-height: 1.5;
    margin-bottom: 5px;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    overflow: hidden;
  }
  .video {
    margin-bottom: 5px;
    img {
      display: block;
      width: 100%;
      height: 170/360 * 100vw;
    }
  }
  .video-layer {
    position: absolute;
    left: 45%;
    top: 45%;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-shrink: 0;
    width: 46/360 * 100vw;
    height: 46/360 * 100vw;
    background-color: rgba(0, 0, 0, 0.5);
      i{
        font-size: 40/360*100vw;
        color: white;
      }
  }
  .post-info {
    font-size: 12px;
    color: #999;
  }
}
</style>
