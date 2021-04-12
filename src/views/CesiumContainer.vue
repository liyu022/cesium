<template>
  <div id="cesiumContainer"></div>
</template>

<script>
import 'cesium/Build/Cesium/Widgets/widgets.css'
import * as Cesium from 'Cesium'
export default {
  name: 'CesiumContainer',
  mounted() {
    /* eslint no-new: */
    Cesium.Ion.defaultAccessToken =
      'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNjMxY2U1Yy0xZGY5LTQxMzAtOGE3OS01MzZiM2Y1ZjcxZGEiLCJpZCI6NTAzMDQsImlhdCI6MTYxNzY3ODE3Nn0.kMkzQBdC1wwzbiEbT-2qwYrYxqyxHU981GSl89BM0dw'
    // const config = {
    //   geocoder: false,
    //   homeButton: false,
    //   sceneModePicker: false,
    //   baseLayerPicker: false,
    //   navigationHelpButton: false,
    //   animation: false,
    //   timeline: false,
    //   fullscreenButton: false,
    //   vrButton: false
    // }
    // const viewer = new Cesium.Viewer('cesiumContainer', config)
    // // 去除版权信息
    // viewer._cesiumWidget._creditContainer.style.display = 'none'
    // 需要进行可视化的数据源的集合
    const config = {
      animation: false, // 是否显示动画控件
      shouldAnimate: true,
      homeButton: false, // 是否显示Home按钮
      fullscreenButton: false, // 是否显示全屏按钮
      baseLayerPicker: false, // 是否显示图层选择控件
      geocoder: false, // 是否显示地名查找控件
      timeline: false, // 是否显示时间线控件
      sceneModePicker: false, // 是否显示投影方式控件
      navigationHelpButton: false, // 是否显示帮助信息控件
      infoBox: false, // 是否显示点击要素之后显示的信息
      requestRenderMode: true, // 启用请求渲染模式
      scene3DOnly: false, // 每个几何实例将只能以3D渲染以节省GPU内存
      sceneMode: 3, // 初始场景模式 1 2D模式 2 2D循环模式 3 3D模式  Cesium.SceneMode
      // fullscreenElement: document.body, //全屏时渲染的HTML元素 暂时没发现用处
      imageryProvider: new Cesium.WebMapTileServiceImageryProvider({
        url: 'http://t0.tianditu.com/img_w/wmts?v=4.0&tk=2303ece9001a4d6ddf48855468a85b5c',
        layer: 'img',
        style: 'default',
        format: 'tiles',
        tileMatrixSetID: 'w',
        credit: new Cesium.Credit('天地图全球影像服务')
      })
    }
    const viewer = new Cesium.Viewer('cesiumContainer', config)
    viewer._cesiumWidget._creditContainer.style.display = 'none'
    viewer.imageryLayers.addImageryProvider(
      new Cesium.WebMapTileServiceImageryProvider({
        url: 'http://t0.tianditu.com/cia_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=cia&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&tk=2303ece9001a4d6ddf48855468a85b5c',
        layer: 'tdtAnnoLayer',
        style: 'default',
        format: 'image/jpeg',
        tileMatrixSetID: 'GoogleMapsCompatible',
        maximumLevel: 13,
        minimumLevel: 1,
        show: false
      })
      // 一： ArcGisMapServerImageryProvider
      // new Cesium.ArcGisMapServerImageryProvider({
      //   url: 'https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer',
      //   enablePickFeatures: false
      // })
      // 二： BingMapsImageryProvider 不可用！
      // new Cesium.BingMapsImageryProvider({
      //   url: 'https://dev.virtualearth.net',
      //   key: 'get-yours-at-https://www.bingmapsportal.com/',
      //   mapStyle: Cesium.BingMapsStyle.AERIAL
      // })
      // 三： createOpenStreetMapImageryProvider
      // Cesium.createOpenStreetMapImageryProvider({
      //   url: 'https://a.tile.openstreetmap.org/'
      // })
      // 四：MapboxImageryProvider  提供了mapbox.satellite、mapbox.streets、mapbox.streets-basic 三种风格 basic不行
      // new Cesium.MapboxImageryProvider({
      //   accessToken: 'sk.eyJ1Ijoiam9saW5lZHUiLCJhIjoiY2tsbm9zdHJxMGt3bjJvbDZqZXdrc2FibCJ9.kNgvWaCz2utF6lmE3fOGHA',
      //   mapId: 'mapbox.streets-basic'
      // })
    )
    // Create an initial camera view
    // eslint-disable-next-line new-cap
    var initialPosition = new Cesium.Cartesian3.fromDegrees(104, 30.674512895646692812, 2631.082799425431)
    // eslint-disable-next-line new-cap
    var initialOrientation = new Cesium.HeadingPitchRoll.fromDegrees(108, 37.987223091598949054, 0.025883251314954971306)
    var homeCameraView = {
      destination: initialPosition,
      orientation: {
        heading: initialOrientation.heading,
        pitch: initialOrientation.pitch,
        roll: initialOrientation.roll
      }
    }
    // Set the initial view
    viewer.scene.camera.setView(homeCameraView)
    viewer.cesiumWidget.screenSpaceEventHandler.removeInputAction(Cesium.ScreenSpaceEventType.LEFT_DOUBLE_CLICK)
    createModel('public/SampleData/models/CesiumAir/Cesium_Air.glb', 0.0)
    function createModel(url, height) {
      viewer.entities.removeAll()
      var position = Cesium.Cartesian3.fromDegrees(108.12121, 34.0503706, height)
      var heading = Cesium.Math.toRadians(135)
      var pitch = 0
      var roll = 0
      var hpr = new Cesium.HeadingPitchRoll(heading, pitch, roll)
      var orientation = Cesium.Transforms.headingPitchRollQuaternion(position, hpr)
      var entity = viewer.entities.add({
        name: url,
        position: position,
        orientation: orientation,
        model: {
          uri: url,
          minimumPixelSize: 128,
          maximumScale: 20000
        }
      })
      viewer.trackedEntity = entity
    }
    // setTimeout(function () {
    //   flyExtent()
    // }, 1000)

    // function flyExtent() {
    //   // 相机看点的角度，如果大于0那么则是从地底往上看，所以要为负值，这里取-30度
    //   var pitch = Cesium.Math.toRadians(-30)
    //   // 给定飞行一周所需时间，比如10s, 那么每秒转动度数
    //   var angle = 360 / 5
    //   // 给定相机距离点多少距离飞行，这里取值为5000m
    //   var distance = 5000
    //   var startTime = Cesium.JulianDate.fromDate(new Date())

    //   var stopTime = Cesium.JulianDate.addSeconds(startTime, 5, new Cesium.JulianDate())

    //   viewer.clock.startTime = startTime.clone() // 开始时间
    //   viewer.clock.stopTime = stopTime.clone() // 结速时间
    //   viewer.clock.currentTime = startTime.clone() // 当前时间
    //   viewer.clock.clockRange = Cesium.ClockRange.CLAMPED // 行为方式
    //   viewer.clock.clockStep = Cesium.ClockStep.SYSTEM_CLOCK // 时钟设置为当前系统时间; 忽略所有其他设置。
    //   // 相机的当前heading
    //   var initialHeading = viewer.camera.heading
    //   var Exection = function TimeExecution() {
    //     // 当前已经过去的时间，单位s
    //     var delTime = Cesium.JulianDate.secondsDifference(viewer.clock.currentTime, viewer.clock.startTime)
    //     var heading = Cesium.Math.toRadians(delTime * angle) + initialHeading
    //     viewer.scene.camera.setView({
    //       destination: position, // 点的坐标
    //       orientation: {
    //         heading: heading,
    //         pitch: pitch
    //       }
    //     })
    //     viewer.scene.camera.moveBackward(distance)
    //     if (Cesium.JulianDate.compare(viewer.clock.currentTime, viewer.clock.stopTime) >= 0) {
    //       viewer.clock.onTick.removeEventListener(Exection)
    //     }
    //   }
    //   viewer.clock.onTick.addEventListener(Exection)
    // }
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
