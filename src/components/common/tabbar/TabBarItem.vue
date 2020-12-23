<template>
  <div class="tab-bar-item" @click="itemClick"><!-- 添加点击监听 -->
    <div v-if="isActive"><slot name="item-icon-active"></slot></div>
    <div v-else><slot name="item-icon"></slot></div>
    <!-- <div v-bind:class="{'active': isActive}"><slot name='item-text'></slot></div> -->
    <div :style="activeStyle"><slot name='item-text'></slot></div>
    <!-- 这里用div包裹插槽：因为替换插槽的时候插槽的属性也会被替换掉，导致没有效果 -->
  </div>
</template>
  
<script>
export default {
  name: "TabBarItem",
  computed: {
    isActive() {
      // return this.$route.path == this.path 
      // return this.$route.path.indexOf(this.path) !== -1 
    },
    activeStyle() {
      return this.isActive ? {color:this.activeColor} : {}
    }
  },
  // 从父组件中获取信息
  props:{
    path: String,
    activeColor:{
      type: String,
      default: 'red'
    }
  },
  methods:{
    itemClick() {
      this.$router.replace(this.path);
    }
  }
}
</script>

<style>
  .tab-bar-item {
    flex-grow: 1;
    text-align: center;
    height: 49px; /* 一般都是49px */
    font-size: 14px;
  }
  .tab-bar-item img {
    width: 24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle;
  }
  /* 动态决定颜色，不能写死 */
  /* .active {
    color: red;
  } */
</style>