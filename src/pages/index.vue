
<template>
  <div>
    <div class="header">
      <div class="logo">
        <span class="iconfont iconnew" ></span>
      </div>
      <router-link to="/search" class="link-search">
        <div class="serach">
          <i class="iconfont iconsearch"></i>
          <span>搜索新闻</span>
        </div>
      </router-link>
      <router-link to="/Personal">
        <span class="iconfont iconwode user"></span>
      </router-link>
    </div>

    <div>
      <van-tabs v-model="active" sticky swipeable>
        <van-tab v-for="(item,index) in categores" :title="item.name" :key="index">
          <van-list
            v-model="item.loading"
            :finished="item.finished"
            finished-text="没有更多了"
            @load="onLoad"
            :immediate-check="false"
          >
            <!-- 文章模块组件，post是单篇文章详情 -->
            <PostCard v-for="(item, index) in item.posts" :key="index" :posts="item" />
          </van-list>
          <van-loading 
            v-if="item.posts.length === 0 && !item.finished"
            size="24px" 
            style='margin-top:20px;'
            vertical 
            type="spinner" 
            color="#1989fa">加载中...</van-loading>
        </van-tab>
      </van-tabs>
    </div>
  </div>
</template>

<script>
import PostCard from "@/components/PostCard";
export default {
   name: "index",
  components: {
    PostCard
  },
  data() {
    return {
      active: localStorage.getItem("token") ? 1 : 0,
      categores: [],
      cid: 999,
      // posts: [],
      // loading: false,
      // finished: false,
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
    //请求栏目的数据
    this.$axios(config).then(res => {
      const { data } = res.data;
      // console.log(data);
      const newData = [];
      // 给每个栏目加四个独立属性
      data.forEach(v => {
        v.posts = [];
        v.loading = false;
        v.finished = false;
        v.pageIndex = 1;
        newData.push(v);
      });

      this.categores = newData;
      // console.log(this.categores);

      // 请求文章
      this.$axios({
        url: `/post?category=${this.cid}&pageIndex=${this.pageIndex}&pageSize=${this.pageSize}`
      }).then(res => {
        // console.log(res);
        const { data } = res.data;
        // console.log(data);

        // 默认赋值给头条的列表
        this.categores[this.active].posts = data;

        this.categores[this.active].pageIndex++;
      });
    });
  },

  methods: {
    onLoad() {
      setTimeout(() => {

        const category = this.categores[this.active];
        console.log(category);

        this.$axios({
          url: `/post?category=${this.cid}&pageIndex=${category.pageIndex}&pageSize=${this.pageSize}`
        }).then(res => {
          // console.log(res);
          const { data } = res.data;

          if (data.length < this.pageSize) {
            category.finished = true;
          }
          category.posts = [...category.posts, ...data];
          category.pageIndex++;
          category.loading = false;
        });
      }, 2000);
    }
  },
  watch: {
    active() {
      //  console.log(this.active)
      this.cid = this.categores[this.active].id;
      console.log(this.cid);

      this.onLoad();
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
  .link-search{
        display: block;
        flex:1;
        margin:0 10px;
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