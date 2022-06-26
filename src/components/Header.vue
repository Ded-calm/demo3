<template>
  <div id="box">
    <h3>购物车</h3>
  </div>
</template>

<script>
export default {
  name: "Header",

  data() {
    return {};
  },

  mounted() {},

  methods: {},
};
</script>

<style lang="less" scoped>
#box {
  width: 100%;
  text-align: center;
  background-color: #3CA9F2;
  // 使用粘性定位 将标题固定在页面顶部
  position: fixed;
  top: 0;
  left: 0;
  // 撑大盒子
  padding: 5px 0;
  // less语法
  h3 {
    color: white;
  }
}
</style> 