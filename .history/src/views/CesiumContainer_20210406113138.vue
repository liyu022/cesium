<template>
  <div id="cesiumContainer"></div>
</template>

<script>
import 'cesium/Build/Cesium/Widgets/widgets.css'
import 'Cesium'
export default {
  name: 'CesiumContainer',
  mounted() {
    /* eslint no-new: */
    Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNjMxY2U1Yy0xZGY5LTQxMzAtOGE3OS01MzZiM2Y1ZjcxZGEiLCJpZCI6NTAzMDQsImlhdCI6MTYxNzY3ODE3Nn0.kMkzQBdC1wwzbiEbT-2qwYrYxqyxHU981GSl89BM0dw'
    const config = {
      geocoder: false,
      homeButton: false,
      sceneModePicker: false,
      baseLayerPicker: false,
      navigationHelpButton: false,
      animation: false,
      timeline: false,
      fullscreenButton: false,
      vrButton: false
    }
    const viewer = new Cesium.Viewer('cesiumContainer', config)
    // 去除版权信息
    viewer._cesiumWidget._creditContainer.style.display = 'none'
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
