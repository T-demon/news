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
        <van-tab v-for="(item,index) in categores" :title="item.name" :key="index">
          <van-list
            :post="item"
            v-model="loading"
            :finished="finished"
            finished-text="没有更多了"
            @load="onLoad"
            :immediate-check="false"
          >
            <!-- 文章模块组件，post是单篇文章详情 -->
            <PostCard v-for="(item, index) in posts" :key="index" :posts="item" />
          </van-list>
        </van-tab>
      </van-tabs>
    </div>
  </div>
</template>

<script>
import PostCard from "@/components/PostCard";
export default {
  components: {
    PostCard
  },
  data() {
    return {
      active: localStorage.getItem("token") ? 1 : 0,
      categores: [],
      cid: 999,
      posts: [],
      loading: false,
      finished: false,
      pageIndex: 1,
      pageSize: 5
    };
  },

  mounted() {
    const config = {
      url: "/category"
    };
    if (localStorage.getItem("token")) {
      config.headers = {
        Authorization: localStorage.getItem("token")
      };
    }
    this.$axios(config).then(res => {
      console.log(res);
      const { data } = res.data;
      this.categores = data;

      this.$axios({
        url: `/post?category=${this.cid}&pageIndex=${this.pageIndex}&pageSize=${this.pageSize}`
      }).then(res => {
        // console.log(res);
        const { data } = res.data;
        // 默认赋值给头条的列表
        this.posts = data;

        this.pageIndex++;
      });
    });
  },

  methods: {
    onLoad: function() {
      setTimeout(() => {
        this.$axios({
          url: `/post?category=${this.cid}&pageIndex=${this.pageIndex}&pageSize=${this.pageSize}`
        }).then(res => {
          // console.log(res);
          const { data } = res.data;

          if (data.length < this.pageSize) {
            this.finished = true;
          }
          this.posts = [...this.posts, ...data];
          this.pageIndex++;
          this.loading = false;
        });
      },2000);
    }
  },
  watch: {
    active() {
      //  console.log(this.active)
      this.cid = this.categores[this.active].id;
      // console.log(this.cid);
    }
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
    margin-left: 10px;
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