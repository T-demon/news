<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-24 15:08:50
 * @LastEditTime: 2019-09-25 15:02:44
 -->
<template>
  <div class="Cell-wrap" @click="$emit('click',$event)">
    <div class="cell">
      <span>{{label}}</span>
      <i>{{type==="password"? "******":text}}</i>
      <span class="iconfont iconjiantou1"></span>
    </div>
  </div>
</template>

<script>
export default {

    props:["label","text","type"]
};
</script>

<style lang="less" scoped>
.Cell-wrap {
  padding-left: 10px;
  .cell {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-right: 10px;
    height: 48 / 360 * 100vw;
    border-bottom: 1px #eee solid;
    i {
      flex: 1;
      font-size:12px;
      color: #b5b5b5;
      text-align: right;
    }
  }
}
</style>
