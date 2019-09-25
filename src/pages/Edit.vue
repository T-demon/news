<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-24 18:56:52
 * @LastEditTime: 2019-09-25 19:06:31
 -->
<template>
  <div>
    <HeaderNormal title="编辑资料" />
    <div class="edit-header">
      <img :src="profile.head_img" alt />
      <!-- vant上传组件 -->
      <van-uploader :after-read="afterRead" class="uploader" />
    </div>
    <!-- 修改昵称 -->
    <CellBar label="昵称" :text="profile.nickname" @click="show1 = !show1" />
    <van-dialog v-model="show1" title="编辑昵称" show-cancel-button @confirm="handlNickname">
      <van-field :value="profile.nickname" placeholder="请输入用户名" ref="nickname" />
    </van-dialog>
    <!-- 修改密码 -->
    <CellBar label="密码" :text="profile.password" type="password" @click="show2 = !show2" />
    <van-dialog v-model="show2" title="编辑密码" show-cancel-button @confirm="handlPassword">
      <van-field :value="profile.password" placeholder="请输入密码" ref="password" />
    </van-dialog>
<!-- 性别修改 -->
    <CellBar label="性别" :text="profile.gender === 1 ? '男' : '女'" @click="show3 = !show3"></CellBar>
    <van-dialog
        v-model="show3"
        title="编辑性别"
        show-cancel-button
        @confirm="handlGender"
        >
        <van-radio-group v-model="genderCache">
            <van-cell-group>
                <van-cell title="男" clickable @click="genderCache = `1`">
                    <van-radio slot="right-icon" name="1" />
                </van-cell>
                <van-cell title="女" clickable @click="genderCache = `0`">
                    <van-radio slot="right-icon" name="0" />
                </van-cell>
            </van-cell-group>
        </van-radio-group>
    </van-dialog>
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
      show1: false,
      show2: false,
      show3:false,
      genderCache:"0"

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
    editProfile(data, callback) {
      if (!data) return;
      this.$axios({
        url: `/user_update/` + localStorage.getItem("user_id"),
        method: "POST",
        // 添加头信息
        headers: {
          Authorization: localStorage.getItem("token")
        },
        data
      }).then(res => {
        const { message } = res.data;
        // 成功的弹窗提示
        if (message === "修改成功") {
          // 传入的回调函数
          // 等于callback && callback();
          if (callback) {
            callback();
          }
          this.$toast.success(message);
        }
      });
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
        this.editProfile({ head_img: data.url});
      });
    },
    // 编辑昵称
    handlNickname: function() {
      const value = this.$refs.nickname.$refs.input.value;
      // console.log(value)
     this.editProfile({ nickname: value}, () => {
            this.profile.nickname = value;
        });
    },
    //编辑密码
    handlPassword: function() {
        const value = this.$refs.password.$refs.input.value;
        this.editProfile({ password: value}, () => {
            this.profile.password = value;
        });
    },
    //编辑性别
    handlGender:function(){
        const gender = +this.genderCache;
        this.editProfile({gender},()=>{
            this.profile.gender=gender;
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
 
