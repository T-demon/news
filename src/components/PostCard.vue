<template>
  <div>
    <div class="post">
      <div class="card-left">
        <div class="post-title">
          {{posts.title}}
          </div>
        <div class="post-info">
          <span>{{posts.user.nickname}}</span>
          <span>52跟帖</span>
        </div>
      </div>
      <div class="card-img">
        <img :src="posts.cover[0].url" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:["posts"],
  mounted(){
   console.log(this.posts)
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
    .post-info{
        font-size: 12px;
        color: #999;
    }
  }
  .card-img {
    img {
      height: 80/360 * 100vw;
      width: 80/360 * 100vw;
      padding-left: 10px;
      object-fit: cover;
    }
  }
}
</style>
