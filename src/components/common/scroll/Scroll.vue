<template>
  <!-- ref是绑定到组件上 -->
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScorll from "better-scroll";
// import PullUp from "@better-scroll/pull-up";

// BScroll.use(PullUp);

export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      scoll: null
    };
  },
  mounted() {
    // 1.创建scroll对象 （需挂载，mounted是vue实例挂载到真实dom上，此时可以获取节点）
    this.scroll = new BScorll(this.$refs.wrapper, {
      observeDOM: true,
      click: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    });

    // 2.监听滚动位置
    this.scroll.on("scroll", position => {
      // console.log(position);
      this.$emit("scroll", position);
    });
    // this.scroll.scrollTo(0, 0);

    // 3.监听上拉事件
    this.scroll.on("pullingUp", () => {
      // console.log("上拉加载更多");
      this.$emit("pullingUp");
    });
    // console.log(this.scroll);
  },
  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll && this.scroll.scrollTo(x, y, time);
    },
    finishPullUp() {
      this.scroll.finishPullUp();
    },
    refresh() {
      // console.log("防抖效果");
      this.scroll && this.scroll.refresh();
    }
  }
};

// console.log(scroll);
</script>

<style>
</style>