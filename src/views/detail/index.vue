<template>
  <div class="scroll-box">
    <div>
      <seller-header :seller="seller"></seller-header>
      <van-tabs v-model="active" sticky animated color="#ffda41">
        <van-tab title="菜单">
          <order></order>
        </van-tab>
        <van-tab title="评价">
          <comment></comment>
        </van-tab>
        <van-tab title="商家">
          <seller :seller="seller"></seller>
        </van-tab>
      </van-tabs>
    </div>
    <cart :seller="seller"></cart>
  </div>
</template>

<script>
import { getStoreById } from "@/api/detail.js";
import sellerHeader from "./seller-header";
import order from "./order";
import BScroll from "better-scroll";
import cart from "./cart.vue";
import comment from "./../comment";
import seller from "./../seller";
export default {
  data() {
    return {
      seller: [],
      active: 0,
      scrollBox: null,
    };
  },
  components: {
    sellerHeader,
    order,
    cart,
    comment,
    seller,
  },
  methods: {
    getStoreMsg() {
      getStoreById({ id: this.$route.query.id }).then((res) => {
        this.seller = res.data;
      });
    },
  },
  mounted() {
    this.scrollBox = new BScroll("./scrollBox", {
      bounce: false,
    });
  },
  created() {
    this.getStoreMsg();
  },
};
</script>

<style lang="scss" scoped>
.scrollBox {
  height: 100vh;
  overflow: hidden;
}
</style>