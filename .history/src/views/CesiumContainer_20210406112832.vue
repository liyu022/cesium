<template>
  <div id="cesiumContainer"></div>
</template>

<script>
import 'cesium/Build/Cesium/Widgets/widgets.css'
import { Viewer } from 'Cesium'
Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNjMxY2U1Yy0xZGY5LTQxMzAtOGE3OS01MzZiM2Y1ZjcxZGEiLCJpZCI6NTAzMDQsImlhdCI6MTYxNzY3ODE3Nn0.kMkzQBdC1wwzbiEbT-2qwYrYxqyxHU981GSl89BM0dw';
export default {
  name: 'CesiumContainer',
  mounted() {
    /* eslint no-new: */
Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNjMxY2U1Yy0xZGY5LTQxMzAtOGE3OS01MzZiM2Y1ZjcxZGEiLCJpZCI6NTAzMDQsImlhdCI6MTYxNzY3ODE3Nn0.kMkzQBdC1wwzbiEbT-2qwYrYxqyxHU981GSl89BM0dw';
    let config = {
      geocoder: false,   // 位置查找工具
      homeButton: false,  // 视角返回初始位置
      sceneModePicker: false,   // 选择视角的模式（球体、平铺、斜视平铺）
      baseLayerPicker: false,    // 图层选择器（地形影像服务）
      navigationHelpButton: false,   // 导航帮助(手势，鼠标)
      animation: false,   // 左下角仪表盘（动画器件）
      timeline: false,   // 底部时间线
      fullscreenButton: false,   // 全屏
      vrButton: false,  // VR
    }
    let viewer = new Cesium.Viewer('container', config);
    // 去除版权信息
    viewer._cesiumWidget._creditContainer.style.display = "none";

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#cesiumContainer {
  width: 100%;
  height: 100%;
}
</style>
