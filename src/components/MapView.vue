<script setup>
import { ref, onMounted } from 'vue'
import * as Cesium from 'cesium'

onMounted(() => {
  initMap()
})

function initMap() {
  const viewer = new Cesium.Viewer('cesium-viewer', {
    geocoder: false,
    homeButton: false,
    sceneModePicker: false,
    baseLayerPicker: false,
    navigationHelpButton: false,
    animation: false,
    timeline: false,
    fullscreenButton: false,
    vrButton: false,
    scene3DOnly: true,
    imageryProviderViewModels: base,
    contextOptions: {
      requestWebgl2: false,
      webgl: {
        alpha: false,
        depth: true,
        stencil: false,
        antialias: true,
        powerPreference: 'high-performance',
        premultipliedAlpha: true,
        preserveDrawingBuffer: false,
        failIfMajorPerformanceCaveat: false,
      },
      allowTextureFilterAnisotropic: true,
    },
  })
  //去掉logo
  viewer._cesiumWidget.creditContainer.style.display = 'none'
  //去掉控制台about:blank报错
  let iframe = document.getElementsByClassName('cesium-infoBox-iframe')[0]
  iframe.setAttribute('sandbox', 'allow-same-origin allow-scripts allow-popups allow-forms')
  iframe.setAttribute('src', '')
  //初始视角
  viewer.camera.setView({
    // destination: Cesium.Cartesian3.fromDegrees(112,10,7000000.0),
    // orientation: {
    //   heading: Cesium.Math.toRadians(30),
    //   pitch: Cesium.Math.toRadians(90),
    //   roll: 0.0,
    // }
  })
}

const base = new Cesium.UrlTemplateImageryProvider({
    //url: 'https://map.geoq.cn/arcgis/rest/services/ChinaOnlineStreetPurplishBlue/MapServer/tile/{z}/{y}/{x}',
    url: 'https://webst02.is.autonavi.com/appmaptile?style=6&x={x}&y={y}&z={z}',
    // tilingScheme: new Cesium.GeographicTilingScheme(),
    // maximumLevel: 17,
    // defaultAlpha: 0,
  });

const cesiumViewerRef = ref(null)

</script>

<template>
  <div class="cesium-container" id="cesium-viewer" ref="cesiumViewerRef"></div>
</template>

<style scoped>
.cesium-container {
  width: 100%;
  height: 100%;
}
</style>
