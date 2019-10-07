<template>
  <div class="foot">
    <div class="footer-a" v-show="!isFocus">
      <input type="text" placeholder="写跟帖" @focus="handleFocus" />

      <!-- <router-link :to="`/comment/${post.id}`">
        <span class="comment">
          <em>1020</em>
          <i class="iconfont iconpinglun-"></i>
        </span>
      </router-link>-->

      <span class="comment" @click="$router.push(`/comment/${post.id}`)">
        <em>{{post.comment_length}}</em>
        <i class="iconfont iconpinglun-"></i>
      </span>

      <i
        class="iconfont iconshoucang"
        :class="{ star_active: post.has_star }"
        @click="$emit('handleStar')"
      ></i>

      <i class="iconfont iconfenxiang"></i>
    </div>

    <div class="footer-b" v-show="isFocus">
      <textarea
        rows="3"
        ref="textarea"
        v-model="value"
        :placeholder="placeholder"
        @blur="handleBlur"
        :autofocus="isFocus"
      ></textarea>
      <span @click="handleSubmit">发送</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["post", "replyComment"],
  data() {
    return {
      isFocus: false,
      // 评论的内容
      value: "",
      placeholder: "写跟帖"
    };
  },
  methods: {
    handleFocus() {
      this.isFocus = true;
    },
    // 输入框失去焦点时候触发
    handleBlur() {
      if (!this.value) {
        this.isFocus = false;

        // 如果有回复的评论，清空回复的评论
        if (this.replyComment) {
          this.$emit("handleReply", null);
          this.placeholder = "写跟帖";
        }
      }
    },
    // 发布评论
    handleSubmit() {
      if (!this.value) {
        return;
      }
      const data = {
        content: this.value
      };

      if (this.replyComment) {
        data.parent_id = this.replyComment.id;
      }

      this.$axios({
        url: "/post_comment/" + this.post.id,
        method: "POST",
        // 添加头信息
        headers: {
          Authorization: localStorage.getItem("token")
        },
        data
      }).then(res => {
        const { message } = res.data;
        console.log(res);
        if (message === "评论发布成功") {
          // 触发父组件方法更新评论的列表
          this.$emit("getComments", this.post.id);
          // 隐藏输入框
          this.isFocus = false;
          this.value = "";
          window.scrollTo(0, 0);
        }
      });
    }
  },
  watch: {
    replyComment() {
        if(this.replyComment){
                this.isFocus = true;
                this.placeholder = '@' + this.replyComment.user.nickname;
            }
    }
  }
};
</script>

<style scoped lang="less">
.foot {
  position: fixed;

  width: 100%;
  bottom: 0px;

  .footer-a {
    padding: 0px 15px;
    width: 100%;
    display: flex;
    justify-content: space-between;
    box-sizing: border-box;
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

