<template>
  <div>
    <div class="app">
      <h1>app父组件里面的内容</h1>
      <h1>v-model的数据{{ person.name }}的工资是{{ money }}</h1>
      <h2>{{ person.age }}</h2>
      <h2>父组件中count数---{{ count }}</h2>
    </div>
    <!-- 通过添加自定义事件实现获取子组件传递过来的值，实现修改数据 -->
    <!-- goToFatherChangeAge为自定义名称，changeFatherAge为处理函数 -->
    <testIndex
      :person="person"
      @goToFatherChangeAge="changeFatherAge"
      v-model:money="money"
    ></testIndex>
  </div>
</template>

<script setup>
  import { provide, reactive, ref } from "vue";
  import testIndex from "./components/testIndex.vue";
  const person = reactive({
    name: "张三",
    age: 18,
  });
  //定义一个ref数据，通过provide传递给childIndex组件
  const count = ref(1);
  provide("count", count);
  // 同时provide也可以传递一个函数，通过函数获取子组件传递过来的值
  provide("changeNum", (num) => {
    count.value += num;
  });
  // 自定义事件的处理函数
  function changeFatherAge(num) {
    person.age += num;
  }

  // 5.定义money数据，通过v-model传递给testIndex组件
  const money = ref(10000);
</script>

<style></style>
