<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 11:04:12
 * @LastEditTime: 2019-09-22 17:19:25
 -->
<template>
  <input
  class="input"
  :placeholder="placeholder"
  :value="value"
  @input="handleInput"
   />
</template>

<script>
export default {
  props: [
      "placeholder",
      "value",
      "name",
      "rule"
  ],
 methods: {
        handleInput(event){
            this.$emit("input", event.target.value)
        }
    }  
}	

</script>

<style lang="less" secped>
input {
  width: 100%;
  height: 38 / 360 * 100vw;
  padding: 20px 0;
  box-sizing: border-box;
  background: #fff;
  border: none;
  border-bottom: 1px #666 solid;
  outline: none;
  font-size:20px; 
}
</style>