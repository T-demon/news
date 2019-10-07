<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 11:04:12
 * @LastEditTime: 2019-09-22 20:35:02
 -->
<template>
<!-- 输入框要实时显示输入状态 所以一个动态的样式 -->
<!-- 加上一个change事件 -->
  <input
  class="input"
  :class="{
        success: status === 'success',
        error: status === 'error'
    }"

  :placeholder="placeholder"
  :value="value"
  :type="type"
  @input="handleInput"
  @change="handleChange"

   />

</template>

<script>
export default {
  data () {
    return {
      // 存放输入框的状态码
      status:''
    }
  },
  // 利用组件里的属性传值
  props: [
      "placeholder",
      "value",
      "name",
      "rule",
      "type",
      "err_message",

  ],
 methods: {
        handleInput(){
          // 通过事件源对象拿到输入框的value值
            const{value} =event.target
            // 触发父组件的input事件
            this.$emit("input", value)
            // 将传递过来的规则对输入款的值进行校验
            if(this.rule){
              if(this.rule.test(value)){
                this.status = "success";
              }else{
                this.status = "error"
              }
            }
        },
        // change事件在输入框数据改变后触发 进行弹窗的错误提示
       handleChange(){
            if(this.err_message && this.status === "error"){
                // alert(this.err_message);
                this.$toast.fail(this.err_message)
            }
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

.success{
    border-color: blue;
}
.error{
    border-color: red;
}
</style>