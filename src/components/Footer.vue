<template>
  <div id="box">
    <div class="allck">
      <label for=""
        ><input
          type="checkbox"
          name=""
          id=""
          :checked="fullck"
          @change="fullChecked"
        />
        全选</label
      >
    </div>
    <div class="sum">合计:<span> 0￥</span></div>
    <div class="pay">结算(0)</div>
  </div>
</template>

<script>
// 导入 兄弟传值js
import bus from "@/components/EventBus";
export default {
  name: "Footer",
  props: {
    fullck: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {};
  },

  mounted() {},

  methods: {
    // 主动全选或反选
    fullChecked(e) {
      // 使用兄弟传值将全选状态转递给App组件
      bus.$emit("fullChecked", e.target.checked);
    },
  },
};
</script>

<style lang="less" scoped>
#box {
  width: 100%;
  min-width: 370px;
  display: flex;
  // 两端对齐
  justify-content: space-between;
  align-items: center;
  width: 100%;
  background-color: #3ca9f2;
  // 使用粘性定位 将底栏固定在页面底部
  position: fixed;
  left: 0;
  bottom: 0px;
  padding: 5px 25px;
  // 盒模型
  box-sizing: border-box;
}
.sum > span {
  color: red;
}
.pay {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 80px;
  padding: 10px;
  background-color: orange;
  border-radius: 40px;
  color: white;
}
</style>