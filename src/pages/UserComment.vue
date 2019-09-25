<template>
  <div>
    <HeaderNormal title="我的跟贴"></HeaderNormal>
    <div class="mycomment" v-for="(item,index) in list" :key="index">
      <div class="time">2019-0-25 10:25</div>
      <div class="parent" v-if="item.parent">
        <div class="parent-title">@:{{item.parent.user.nickname}}</div>
        <div class="parent-content">{{item.parent.content}}</div>
      </div>

      <div class="content">{{item.content}}</div>

      <router-link to="#" class="content-link">
        <P>原文：{{item.post.title}}</P>
        <span class="iconfont iconjiantou1"></span>
      </router-link>
    </div>
  </div>
</template>

<script>
import HeaderNormal from "@/components/HeaderNormal";
export default {
  components: {
    HeaderNormal
  },
  data() {
    return {
      list: []
    };
  },
  mounted() {
    this.$axios({
      url: "/user_comments",
      headers: {
        Authorization: localStorage.getItem("token")
      }
    }).then(res => {
      console.log(res);
      const { data } = res.data;
      this.list = data;
    });
  }
};
</script>

<style lang="less" scoped>
.mycomment {
  padding: 20px;
  border-bottom: 1px solid gray;
  .time {
    font-size: 14px;
    color: #999;
    margin-bottom: 10px;
  }
  .parent {
    background-color: #e5e5e5;
    color: #999;
    padding: 10px;
    line-height: 1.5;
    margin-bottom: 20px;
    .parent-title {
      font-size: 14px;
      margin-bottom: 5px;
    }
  }
  .content {
    margin-bottom: 10px;
  }
  .content-link {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #999;
    margin-bottom: 10px;
    p {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }
}
</style>
