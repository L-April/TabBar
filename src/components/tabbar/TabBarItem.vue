<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
    <!-- <div :class="{ active: isActive }">
      <slot name="item-text"></slot>
    </div> -->
    <!-- <img src="../../assets/tabbar/home.svg" alt="首页" /> 
      <div>首页</div> -->
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props: {
    path: String,
    activeColor: {
      type: String,//类型
      default: "pink",//默认值
    },
  },
  data() {
    return {
      //isActive: true,
    };
  },
  computed: {
    isActive() {
      return this.$route.path.indexOf(this.path) !== -1;
    },
    activeStyle(){
      return this.isActive?{color:this.activeColor}:{}
    }
  },
  methods: {
    itemClick() {
      console.log("itemClick");
      if (this.$route.path == this.path) {
        return;
      }
      this.$router.replace(this.path); //浏览器有返回用push，否则用replace
    },
  },
};
</script>

<style scoped>
.tab-bar-item {
  flex: 1; /**平分布局 */
  text-align: center;
  height: 49px;
  font-size: 14px;
}

.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  vertical-align: middle; /*去掉图片默认下边有3px */
  margin-bottom: 2px;
}
/* .active {
  color: red;
} */
</style>