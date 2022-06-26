//计数组件
<template>
  <div id="box">
    <div class="btn">
      <div class="btn-sub" @click="sub">-</div>
      <div class="num">{{ goods_count }}</div>
      <div class="btn-add" @click="add">+</div>
    </div>
  </div>
</template>

<script>
// 导入 兄弟传值js
import bus from "@/components/EventBus";
export default {
  name: "Count",
  props: {
    // 接收父组件传递的商品数量
    goods_count: {
      type: Number,
      default: 1,
    },
    goods_id: {
      type: Number,
    },
  },
  data() {
    return {};
  },

  mounted() {},

  methods: {
    // 商品数量+1
    add() {
      // 使用兄弟传值直接将需要修改的结果及商品id传递给App组件
      bus.$emit("share", {
        id: this.goods_id,
        value: this.goods_count + 1,
      });
    },
    sub() {
      // 判断当前商品数量是否大于1
      if (this.goods_count > 1) {
        // 使用兄弟传值直接将需要修改的结果及商品id传递给App组件
        bus.$emit("share", {
          id: this.goods_id,
          value: this.goods_count - 1,
        });
      }
    },
  },
};
</script>

<style lang="less" scoped>
#box {
  margin-right: 10px;
}
.btn {
  display: flex;
  div {
    padding: 0 5px;
    font-size: 18px;
    font-weight: 500;
  }
}
.num {
  width: 20px;
  text-align: center;
  border: 1px solid #ada9a1;
}
</style>