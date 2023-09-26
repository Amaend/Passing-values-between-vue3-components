<template>
  <div class="son">
    <h1>son组件</h1>
    <!-- 组件通信 -->
    <p>该信息将用于组件通信{{ msg }}</p>
  </div>
</template>

<script setup>
  import { ref, defineExpose } from "vue";
  // 定义两条数据用于实现组件通信
  const msg = ref("hello");
  //   定义一个函数一并暴露出去
  const sonFuncton = () => {
    console.log("son组件里面的方法");
  };
  //   需要通过defineExpose将msg暴露出去
  defineExpose({ msg, sonFuncton });
</script>

<style lang="less" scoped>
  .son {
    background-color: #fff;
    border: 1px solid #ccc;
    margin: 10px;
  }
</style>
