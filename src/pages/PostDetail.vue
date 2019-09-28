<template>
  <div>
    <div class="detail">
      <div class="detail-header">
        <span class="iconfont iconjiantou2"></span>
        <i class="iconfont iconnew"></i>
        <span class="gzbtn">关注</span>
      </div>
      <h3>火星时报火星时报火星时报火星时报火星时时报</h3>
      <div class="detail-info">
        <span>火星时报</span>
        <span>201-10-10</span>
      </div>
      <div class="detail-content">
        火星时报火星时报火星时报火
        星时报火星时报火星时星时报火星时
        报火星时报火星时报火星时报火星时报
        火星时星时报火星时报火星时报火星时报火星时报火星时报火星时星时报
      </div>
      <div class="post-btns">
        <span>
          <i class="iconfont icondianzan"></i>
          112
        </span>
        <span>
          <i class="iconfont iconweixin"></i>
          微信
        </span>
      </div>
    </div>
    <div class="foot">
      <PostFooter></PostFooter>
    </div>
  </div>
</template>

<script>
import PostFooter from "@/components/PostFooter";
export default {
  components: {
    PostFooter
  }
};
</script>

<style lang="less" scoped>
.detail {
  padding: 0px 20px;
  border-bottom: 3px solid #999;
  padding-bottom: 20px;
  .detail-header {
    height: 60/360 * 100vw;
    display: flex;
    justify-content: space-between;
    align-items: center;
    i {
      flex: 1;
      font-size: 55/360 * 100vw;
    }
    .gzbtn {
      display: block;
      padding: 5px 20px;
      background-color: #ff0000;
      font-size: 12px;
      color: #fff;
      border-radius: 50px;
    }
  }
  .detail-info {
    font-size: 12px;
    color: #999;
    padding: 10px 0;
  }
  .detail-content {
    margin-top: 10px;
    font-size: 14px;
    line-height: 1.5;
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