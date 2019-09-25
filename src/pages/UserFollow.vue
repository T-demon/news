<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-25 19:12:35
 * @LastEditTime: 2019-09-25 19:40:32
 -->
<template>
  <div>
    <HeaderNormal title="我的关注"></HeaderNormal>
    <div class="item">
      <div class="headimg">
        <img src="../../static/timg.gif" />
      </div>
      <div class="item-center">
        <p>火星情报局</p>
        <span>2019-09-25</span>
      </div>
      <span class="follow">取消关注</span>
    </div>
  </div>
</template>

<script>
import HeaderNormal from "@/components/HeaderNormal";
export default {
  components: {
    HeaderNormal
  }
};
</script>

<style lang="less" scoped>
.item {
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .item-center {
    flex: 1;
    padding-left: 10px;
  }
  .headimg {
    border-radius: 50%;
    background-color: #e5e5e5;
    img {
      width: 40/360 * 100vw;
      height: 40/360 * 100vw;
    }
  }
  .follow {
      display: block;
      background: #e5e5e5;
      padding: 0 10px;
      height: 26px;
      line-height: 26px;
      font-size: 12px;
      border-radius: 50px;
    }
}
</style>
