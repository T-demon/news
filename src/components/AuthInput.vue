<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 11:04:12
 * @LastEditTime: 2019-09-22 20:35:02
 -->
<template>
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
      status:''
    }
  },
  props: [
      "placeholder",
      "value",
      "name",
      "rule",
      "type",
      "err_message",

  ],
 methods: {
        handleInput(event){
            const{value} =event.target
            this.$emit("input", value)
            if(this.rule){
              if(this.rule.test(value)){
                this.status = "success";
              }else{
                this.status = "error"
              }
            }
        },
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