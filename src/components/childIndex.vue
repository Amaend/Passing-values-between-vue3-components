<template>
  <div class="child">
    <h3>孩子属性</h3>
    <h2>通过provide传递下来的count属性---{{ count }}</h2>
    <button @click="changeCount">修改count的值</button>
  </div>
</template>

<script setup>
  // 4.通过provide与inject实现组件之间的通信
  import { inject, ref } from "vue";
  // 通过inject引入属性
  const count = ref(inject("count"));
  // 同样通过inject引入的方法
  const change = inject("changeNum");
  // 方法一修改通过inject引入的属性的值，将该值转变为ref响应式数据
  //   function changeCount() {
  //     count.value++;
  //   }
  function changeCount() {
    change(2);
  }
</script>

<style lang="less" scoped>
  .child {
    background-color: #f3f3f3;
    padding: 10px;
  }
</style>
