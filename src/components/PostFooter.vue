<template>
  <div class="foot">
    <div class="footer-a" v-show="!isFocus">
      <input type="text" placeholder="写跟帖" @focus="handleFocus" />

      <router-link :to="`/comment/${post.id}`">
        <span class="comment">
          <em>1020</em>
          <i class="iconfont iconpinglun-"></i>
        </span>
      </router-link>

      <i
        class="iconfont iconshoucang"
        :class="{ star_active: post.has_star }"
        @click="$emit('handleStar')"
      ></i>

      <i class="iconfont iconfenxiang"></i>
    </div>

    <div class="footer-b" v-show="isFocus">
      <textarea rows="3" ref="textarea" @blur="isFocus = false" :autofocus="isFocus"></textarea>
      <span>发送</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["post"],
  data() {
    return {
      isFocus: false
    };
  },

  methods: {
    handleFocus() {
      console.log(123);
      this.isFocus = true;
    }
  }
};
</script>

<style scoped lang="less">
.foot {
  position: fixed;
  padding: 0px 15px;
  width: 100%;
  bottom: 0px;
  box-sizing: border-box;
  .footer-a {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #fff;
    input {
      width: 60%;
      height: 36 / 360 * 100vw;
      background: #eee;
      border: none;
      font-size: 12px;
      padding: 0 15px;
      border-radius: 50px;
    }
    .comment {
      display: block;
      position: relative;
      em {
        position: absolute;
        display: block;
        background: red;
        border-radius: 50px;
        color: #fff;
        padding: 0 5px;
        font-size: 10px;
        height: 14px;
        line-height: 14px;
        left: 0;
        top: -5px;
      }
    }
    .iconfont {
      font-size: 24px;
    }
    .star_active {
      color: yellow;
    }
  }
  .footer-b {
    box-sizing: border-box;
    padding: 10px;
    display: flex;
    align-items: flex-end;
    textarea {
      width: 260 / 360 * 100vw;
      background: #eee;
      padding: 10px;
      box-sizing: border-box;
      border: none;
      border-radius: 8px;
      resize: none;
    }
    span {
      font-size: 12px;
      background: red;
      width: 60 / 360 * 100vw;
      height: 26 / 360 * 100vw;
      line-height: 26 / 360 * 100vw;
      color: #fff;
      text-align: center;
      border-radius: 50px;
    }
  }
}
</style>

