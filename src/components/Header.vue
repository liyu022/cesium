<template>
  <div class="nav">
    <div class="content">
      <div class="left">
        <div
          class="item"
          @click="navSelect(item)"
          :class="{ active: item.active }"
          v-for="item in leftNav"
          :key="item.text"
        >
          {{ item.text }}
        </div>
      </div>
      <div class="title"></div>
      <div class="right">
        <div
          class="item"
          @click="navSelect(item)"
          :class="{ active: item.active }"
          v-for="item in rightNav"
          :key="item.text"
        >
          {{ item.text }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'Header',
  data() {
    return {
      leftNav: [
        { text: '移动执法', active: true, url: '/' },
        { text: '移动源监测', active: false, url: '/ydyjc' },
        { text: '应急指挥', active: false, url: '/yjzh' }
      ],
      rightNav: [
        { text: '重点污染源', active: false, url: '/zdwry' },
        { text: '网格化管理', active: false, url: '/wghgl' },
        { text: '污染源扩散模型', active: false, url: '/wgfgl' }
      ]
    }
  },
  methods: {
    navSelect: function(item) {
      this.leftNav.forEach((item) => (item.active = false))
      this.rightNav.forEach((item) => (item.active = false))
      item.active = true
      this.$router.push(item.url)
    }
  }
}
</script>

<style lang="scss" scoped>
.nav {
  width: 1920px;
  height: 160px;
  position: absolute;
  z-index: 99;
  .content {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 60px;
    width: 1920px;
    .item {
      width: 175px;
      height: 60px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 16px;
      font-family: Microsoft YaHei;
      font-weight: 400;
      color: #ffffff;
      text-shadow: 0px 3px 5px rgba(0, 86, 235, 0.98);
      cursor: pointer;
    }
    .active {
      background-image: url('../assets/nav/nav_select.png');
      background-repeat: no-repeat;
    }
    .left {
      height: 60px;
      display: flex;
    }
    .title {
      width: 500px;
      height: 60px;
      background-image: url('../assets/nav/nav_title.png');
      background-position: center 20px;
      background-repeat: no-repeat;
    }
    .right {
      height: 60px;
      display: flex;
    }
  }
}
</style>
