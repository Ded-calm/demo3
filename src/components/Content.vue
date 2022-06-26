<template>
  <div id="con">
    <!-- 复选框 -->
    <div class="ckbtn">
      <!-- 绑定change事件 将勾选状态传递给父组件并在父组件进行修改 -->
      <input
        type="checkbox"
        name=""
        id=""
        :checked="goods.goods_state"
        @change="goodState"
      />
    </div>
    <!-- 图片展示 -->
    <div class="pic">
      <img :src="goods.goods_img" alt="" srcset="" />
    </div>
    <!-- 标题及按钮 -->
    <div class="title">
      <div class="text">{{ goods.goods_name }}</div>
      <div class="price">
        <div>{{ goods.goods_price }}￥</div>
        <!-- 将商品数量以及商品id传给计数子组件 -->
        <Count :goods_count="goods.goods_count" :goods_id="goods.id"></Count>
      </div>
    </div>
  </div>
</template>

<script>
// 导入计数组件
import Count from "@/components/Count.vue";
export default {
  name: "Content",
  props: {
    goods: {
      type: Object,
      require: true,
    },
  },
  data() {
    return {};
  },

  mounted() {},

  methods: {
    // 商品状态
    goodState(e) {
      //   向父组件传递当前商品勾选状态;
      this.$emit("changeState", {
        // 事件对象的勾选状态
        state: e.target.checked,
        // 当前组件实例的商品id
        id: this.goods.id,
      });
    },
  },
  components: {
    Count,
  },
};
</script>

<style lang="less" scoped>
#con {
  display: flex;
  align-items: center;
  width: 100%;
  // 距离顶部24.8px
  margin-top: 34.8px;
  border-bottom: 1px solid #ada9a1;
}
.ckbtn {
  width: 50px;
  text-align: center;
}
.pic {
  flex: 2;
}
.pic img {
  width: 100%;
}
.title {
  flex: 6;
  padding: 5px 0px 5px 10px;
}
.title > .text {
  font-size: 14px;
  height: 60px;
  font-weight: 500;
}
.title > .price {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 30px;
}
.title > .price > div:nth-child(1) {
  color: red;
}
</style>