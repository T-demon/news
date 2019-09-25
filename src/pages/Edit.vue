<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-24 18:56:52
 * @LastEditTime: 2019-09-25 16:55:42
 -->
<template>
  <div>
    <HeaderNormal title="编辑资料" />
    <div class="edit-header">
      <img :src="profile.head_img" alt />
      <!-- vant上传组件 -->
      <van-uploader :after-read="afterRead" class="uploader" />
    </div>
    
    <CellBar label="昵称" :text="profile.nickname" @click="show1 = !show1"/>
    <van-dialog
        v-model="show1"
        title="编辑昵称"
        show-cancel-button
        >
        <!-- value读取昵称 -->
        <van-field :value="profile.nickname" placeholder="请输入用户名" />
    </van-dialog>

    <CellBar label="密码" :text="profile.password" type="password"></CellBar>
    <CellBar label="性别" text="男"></CellBar>
  </div>
</template>

<script>
import CellBar from "@/components/CellBar";
import HeaderNormal from "@/components/HeaderNormal";

export default {
  components: {
    CellBar,
    HeaderNormal
  },
  data() {
    return {
      profile: {},
      show1:false
    };
  },
  mounted() {
    this.$axios({
      url: "/user/" + localStorage.getItem("user_id"),
      headers: {
        Authorization: localStorage.getItem("token")
      }
    }).then(res => {
      const { data } = res.data;
      console.log(res);
      this.profile = data;
      if (data.head_img) {
        this.profile.head_img =
          this.$axios.defaults.baseURL + this.profile.head_img;
      } else {
        this.profile.head_img = "./static/男头像.png";
      }
    });
  },

  methods: {
    handelback: function() {
      this.$router.push("/");
    },
    //处理图片
    afterRead: function(file) {
      //   console.log(file);
      //构建表单是数据
      const formData = new FormData();
      formData.append("file", file.file);

      this.$axios({
        url: "/upload",
        method: "POST",
        headers: {
          Authorization: localStorage.getItem("token")
        },
        data: formData
      }).then(res => {
        //   console.log(res.data)
        const { data } = res.data;

        this.profile.head_img = this.$axios.defaults.baseURL + data.url;
        //修改数据库图片
        this.$axios({
          url: `/user_update/` + localStorage.getItem("user_id"),
          method: "POST",
          // 添加头信息
          headers: {
            Authorization: localStorage.getItem("token")
          },
          data: {
            head_img: data.url
          }
        }).then(res => {
          const { message } = res.data;
          // 成功的弹窗提示
          if (message === "修改成功") {
            this.$toast.success(message);
          }
        })
      })
    }
  }
};
</script>
  

<style lang="less" scoped>
.edit-header {
  padding: 20px;
  align-items: center;
  justify-content: center;
  display: flex;
  position: relative;
  .uploader {
    position: absolute;
    opacity: 0;
  }
  img {
    width: 70 / 360 * 100vw;
    height: 70 / 360 * 100vw;
    border-radius: 50%;
    display: block;
    margin: 20px auto;
    //   margin-bottom: 20px;
  }
  /deep/ .van-uploader__upload {
    width: 70 / 360 * 100vw;
    height: 70 / 360 * 100vw;
  }
}
</style>>
 
