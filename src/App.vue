<script setup>
import { Scene, LineLayer, PointLayer, Popup } from '@antv/l7'
import { GaodeMap } from '@antv/l7-maps'
</script>

<template>
  <div><h2 class="text">蹭饭地图</h2></div>
  <div style="width: 100vw; height: 90vh; justify-content: center;position: relative" id="map" />
</template>

<script>

const data = [
  {
    "name": "北京大学",
    "longitude": 116.316833,
    "latitude": 39.998877,
    "count": 7,
    "num": "01、03、14、20、22、31、45"
  },
  {
    "name": "北京航空航天大学",
    "longitude": 116.353792,
    "latitude": 39.98766,
    "count": 1,
    "num": "16"
  },
  {
    "name": "北京理工大学",
    "longitude": 116.322726,
    "latitude": 39.966659,
    "count": 1,
    "num": "10"
  },
  {
    "name": "电子科技大学",
    "longitude": 103.937404,
    "latitude": 30.756035,
    "count": 1,
    "num": "28"
  },
  {
    "name": "东南大学",
    "longitude": 118.70378,
    "latitude": 32.162734,
    "count": 1,
    "num": "51"
  },
  {
    "name": "国防科技大学",
    "longitude": 113.005966,
    "latitude": 28.235561,
    "count": 1,
    "num": "15"
  },
  {
    "name": "华东理工大学",
    "longitude": 121.430226,
    "latitude": 31.149538,
    "count": 1,
    "num": "25"
  },
  {
    "name": "南方科技大学",
    "longitude": 114.005913,
    "latitude": 22.603944,
    "count": 2,
    "num": "18、37"
  },
  {
    "name": "南京大学",
    "longitude": 118.786007,
    "latitude": 32.06143,
    "count": 3,
    "num": "07、21、48"
  },
  {
    "name": "南京理工大学",
    "longitude": 118.863418,
    "latitude": 32.03162,
    "count": 1,
    "num": "19"
  },
  {
    "name": "南开大学",
    "longitude": 117.17546,
    "latitude": 39.109442,
    "count": 2,
    "num": "02、41"
  },
  {
    "name": "清华大学",
    "longitude": 116.333374,
    "latitude": 40.009645,
    "count": 5,
    "num": "04、05、06、24、36"
  },
  {
    "name": "上海交通大学",
    "longitude": 121.439446,
    "latitude": 31.205568,
    "count": 2,
    "num": "47、43"
  },
  {
    "name": "上海科技大学",
    "longitude": 121.601394,
    "latitude": 31.182971,
    "count": 1,
    "num": "34"
  },
  {
    "name": "同济大学",
    "longitude": 121.505829,
    "latitude": 31.285099,
    "count": 1,
    "num": "11"
  },
  {
    "name": "西安电子科技大学",
    "longitude": 108.923313,
    "latitude": 34.236646,
    "count": 2,
    "num": "27、38"
  },
  {
    "name": "西安交通大学",
    "longitude": 108.990166,
    "latitude": 34.252359,
    "count": 8,
    "num": "28、12、17、23、29、33、42、49"
  },
  {
    "name": "西北工业大学",
    "longitude": 108.923507,
    "latitude": 34.248345,
    "count": 2,
    "num": "35、40"
  },
  {
    "name": "浙江大学",
    "longitude": 120.092406,
    "latitude": 30.308304,
    "count": 3,
    "num": "26、30、50"
  },
  {
    "name": "中国科学技术大学",
    "longitude": 117.276137,
    "latitude": 31.842919,
    "count": 1,
    "num": "39"
  },
  {
    "name": "中国人民大学",
    "longitude": 116.319769,
    "latitude": 39.976546,
    "count": 2,
    "num": "29、52"
  },
  {
    "name": "中央财经大学",
    "longitude": 116.349163,
    "latitude": 39.965211,
    "count": 1,
    "num": "44"
  }
]

async function initMap() {
  // const response = await fetch(
  //   'https://gw.alipayobjects.com/os/basement_prod/893d1d5f-11d9-45f3-8322-ee9140d288ae.json',
  // );
  const scene = new Scene({
    id: 'map',
    map: new GaodeMap({
      center: [108.4, 31.258134],
      zoom: 4,
      pitch: 10,
      style: 'normal',
      rotateEnable: false,
    }),
  });
  scene.addImage(
    '00',
    'https://gw.alipayobjects.com/mdn/rms_fcd5b3/afts/img/A*LTcXTLBM7kYAAAAAAAAAAAAAARQnAQ',
  );
  // const data = await response.json();
  const imageLayer = new PointLayer({
  })
    .source(data, {
      parser: {
        type: 'json',
        x: 'longitude',
        y: 'latitude',
      },
    })
    .shape('00')
    .active(false)
    .size(18);
  scene.addLayer(imageLayer);
  imageLayer.on('mousedown', (e) => {
    console.log('mousedown', e);
  });
  const popup = new Popup({
  });

  scene.addPopup(popup);
  imageLayer.on('click', (e) => {
    console.log(e)
    const { lng, lat } = e.lngLat

    popup.setOptions({
      title: e.feature.name,
      html: e.feature.num,
      lngLat: {
        lng,
        lat,
      },
    });

  });
}

initMap();
</script>

<style>
h2.text {
  text-align: center;
}
</style>
