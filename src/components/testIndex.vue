<template>
  <div class="son">
    <h1>子组件里面的数据内容</h1>
    <!-- 这里可以不用写props名 -->
    <h1>{{ props.person.name }}</h1>
    <!-- 绑定事件，实现自定义事件传值 -->
    <h1>{{ person.age }}</h1>
    <button @click="changeAge">点击修改年龄</button>
    <childIndex></childIndex>
    <!-- 引入son组件实现ref传递数据，实现组件通信 -->
    <span>son组件通过ref传递而来的数据{{ refData }}</span>
    <sonIndex ref="sonRef"></sonIndex>
    <!-- 通过v-model传递而来的数据 -->
    <span>通过v-model从父组件传递下来的值{{ money }}</span>
    <button @click="changeObjInfo">点击修改obj中的数据</button>
  </div>
</template>

<script setup>
  // 导入sonIndex组件
  import sonIndex from "./sonIndex.vue";
  // 导入childIndex组件
  import childIndex from "./childIndex.vue";
  // 1.父组件传递子组件使用props参数接收
  //在子组件中获取父组件传递过来的数据，必须通过props来获取
  // 而通过setup定义的script标签必须通过defineProps来获取必须通过props来接收
  // 注意：setup中不能使用this
  // 而通过defineProps定义的变量，父组件传递过来的数据为响应式数据则子组件获取到的一样是响应式数据
  import { defineProps, defineEmits, ref, onMounted } from "vue";
  const props = defineProps(["person", "money"]);

  // 2.子组件传递给父组件的数据，需通过自定义事件触发
  // 通过defineEmits来创建自定义事件，通过emit来触发自定义事件
  const emit = defineEmits(["goToFatherChangeAge", "update:money"]);
  let changeAge = () => {
    // 触发自定义事件，实现子组件传递给父组件的数据
    emit("goToFatherChangeAge", 1);
  };

  // 3.子组件传递给父组件的数据，需通过ref传递
  // 3.1 子组件中通过ref定义一个变量，并传递给父组件
  let sonRef = ref(null);
  // 定义生命周期钩子函数
  // 3.2 父组件通过ref获取子组件中定义的变量
  // 定义变量用来接收ref传递过来的数据
  const refData = ref(null);
  onMounted(() => {
    console.log(sonRef.value);
    refData.value = sonRef.value.msg;
  });

  // 通过v-model修改数据
  function changeObjInfo() {
    emit(
      "update:money",
      // 添加一个立即执行函数，返回一个函数，函数中返回props中定义的money
      (() => {
        return props.money + 100;
      })()
    );
  }
</script>

<style lang="less" scoped>
  .son {
    background-color: pink;
    padding: 10px;
  }
</style>
