<!--
 * @Describe: 
 * @Author: Tang
 * @Date: 2019-09-22 19:24:11
 * @LastEditTime: 2019-09-22 19:56:23
 -->
<template>
  <div 
  class="button" 
  @click="handleClick">
    {{text}}
  </div>
</template>

<script>
export default {
    props:["text"],
    methods:{
       handleClick(event){
           this.$emit("click",event)
       } 
    }
}


</script>


<style lang="less" scoped>
    .button{
        width: 100%;
        height: 48/360*100vw;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #cc3300;
        color: white;
        border-radius: 50px;
        font-style: 20px;
    }

</style>