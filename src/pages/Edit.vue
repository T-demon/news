<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-24 18:56:52
 * @LastEditTime: 2019-09-25 14:39:22
 -->
<template>
  <div>
    <div class="edit-header">
      <HeaderNormal title="编辑资料" />
    </div>
    <img :src="profile.head_img" alt />
    <CellBar label="昵称" :text="profile.nickname"></CellBar>
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
      profile: {}
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
    }
  }
};
</script>
  

<style lang="less" scoped>
.edit-header {
  padding: 20px 10px;
  align-items: center;
  display: flex;
  span {
    flex: 1;
    text-align: center;
    font-weight: 600;
  }
}
img {
  width: 70 / 360 * 100vw;
  height: 70 / 360 * 100vw;
  border-radius: 50%;
  display: block;
  margin: 20px auto;
  //   margin-bottom: 20px;
}
</style>>
 
