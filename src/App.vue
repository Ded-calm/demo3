<template>
  <div id="app">
    <Header></Header>
  </div>
</template>

<script>
// 导入头部组件
// D:\VueCode\vueDemo03\demo3\src\components\Header.vue
import Header from "@/components/Header.vue";
export default {
  name: "App",

  data() {
    return {};
  },

  // 生命周期函数
  mounted() {},

  methods: {},

  components: {
    Header,
  },
};
</script>

<style scoped>
#app {
  width: 60%;
  /* 居中 */
  margin: 0 auto;
  background-color: #f2f2f2;
}
</style>