<template>
  <div id="app">
    <!-- 头部组件 -->
    <Header></Header>
    <!-- 内容主体组件 -->
    <Content
      v-for="item in cartlist"
      :key="item.id"
      :goods="item"
      @changeState="ckstate"
    ></Content>
    <!-- 底部组件 -->
    <!-- 将所有商品勾选状态传递 fullstate计算属性 -->
    <Footer :fullck="fullstate"></Footer>
  </div>
</template>

<script>
// 导入ajix
import axios from "axios";
// 导入 兄弟传值js
import bus from "@/components/EventBus";
// 导入头部组件
import Header from "@/components/Header.vue";
// 导入内容主体组件
import Content from "@/components/Content.vue";
// 导入底部组件
import Footer from "@/components/Footer.vue";
export default {
  name: "App",

  data() {
    return {
      cartlist: [],
    };
  },

  // 生命周期函数
  created() {
    // 发起ajix请求
    this.initCartList();
    // 接收Count兄弟组件传递的商品数量
    bus.$on("share", (newVal) => {
      // 修改数据
      // 调用 数组的some方法变量整个数组
      this.cartlist.some((item) => {
        // 遍历到数组中单个对象进行判断id是否相等
        if (item.id == newVal.id) {
          // 匹配成功则修改商品数量
          item.goods_count = newVal.value;
        }
      });
    });
    // 接收Footer兄弟组件传递的全选状态
    bus.$on("fullChecked", (state) => {
      // 修改数据
      // 调用 数组的some方法变量整个数组
      this.cartlist.some((item) => {
        // 遍历到数组中单个对象进行状态修改
        item.goods_state = state;
      });
    });
  },
  mounted() {},

  methods: {
    // 封装请求列表数据的方法
    // 异步请求
    async initCartList() {
      // 解构数据data后赋值给res
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      this.cartlist = res.list;
    },
    // 修改商品勾选状态
    ckstate(val) {
      // 修改数据
      // 调用 数组的some方法变量整个数组
      this.cartlist.some((item) => {
        // 遍历到数组中单个对象进行判断id是否相等
        if (item.id == val.id) {
          // 匹配成功则修改商品数量
          item.goods_state = val.state;
        }
      });
    },
  },

  // 注册组件
  components: {
    Header,
    Content,
    Footer,
  },

  // 计算属性
  computed: {
    // 页面数据发生变化则触发计算属性方法
    // 使用计算属性实现全选状态
    fullstate() {
      // 判断数组中所有商品的勾选状态如果都为true则表示为全选状态 返回true
      return this.cartlist.every((item) => item.goods_state == true);
    },
    // 计算被勾选商品价格合计
    priceTotal() {
      let total = 0;
      this.cartlist.some((item) => {
        this.cartlist.some((item) => {
          // 遍历到数组中单个对象进行判断是否被勾选
          if (item.goods_state == true) {
            // 匹配成功则求和商品总价
            total += item.goods_price * item.goods_count;
          }
        });
      });
      console.log(total);
      return total;
    },
  },
};
</script>

<style lang="less" scoped>
/deep/ * {
  padding: 0;
  margin: 0;
}

#app {
  width: 100%;
  max-width: 780px;
  min-width: 370px;
  margin: 0 auto;
  padding-bottom: 20px;
}
</style>