<script setup>
import { Scene, LineLayer, PointLayer, Popup } from '@antv/l7'
import { GaodeMap } from '@antv/l7-maps'
</script>

<template>
  <div><h2 class="text">蹭饭地图</h2></div>
  <div style="width: 100%; height: 96vh; justify-content: center;position: relative" id="map" />
</template>

<script>

const data = [
  {
    "name": "北京大学",
    "longitude": 116.311800,
    "latitude": 39.992766,
    "count": 7,
    "num": "01、03、14、20、22、31、45"
  },
  {
    "name": "北京航空航天大学",
    "longitude": 116.347792,
    "latitude": 39.98266,
    "count": 1,
    "num": "16"
  },
  {
    "name": "北京理工大学",
    "longitude": 116.314726,
    "latitude": 39.960659,
    "count": 1,
    "num": "10"
  },
  {
    "name": "电子科技大学",
    "longitude": 103.930404,
    "latitude": 30.750035,
    "count": 1,
    "num": "28"
  },
  {
    "name": "东南大学",
    "longitude": 118.82248,
    "latitude": 31.888974,
    "count": 1,
    "num": "51"
  },
  {
    "name": "国防科技大学（精确位置不详）",
    "longitude": 113.000966,
    "latitude": 28.227561,
    "count": 1,
    "num": "15"
  },
  {
    "name": "华东理工大学",
    "longitude": 121.424226,
    "latitude": 31.144538,
    "count": 1,
    "num": "25"
  },
  {
    "name": "南方科技大学",
    "longitude": 114.001913,
    "latitude": 22.599944,
    "count": 2,
    "num": "18、37"
  },
  {
    "name": "南京大学",
    "longitude": 118.779007,
    "latitude": 32.05543,
    "count": 3,
    "num": "07、21、48"
  },
  {
    "name": "南京理工大学",
    "longitude": 118.856418,
    "latitude": 32.02862,
    "count": 1,
    "num": "19"
  },
  {
    "name": "南开大学",
    "longitude": 117.16846,
    "latitude": 39.104442,
    "count": 2,
    "num": "02、41"
  },
  {
    "name": "清华大学",
    "longitude": 116.325074,
    "latitude": 40.003000,
    "count": 5,
    "num": "04、05、06、24、36"
  },
  {
    "name": "上海交通大学",
    "longitude": 121.432446,
    "latitude": 31.198868,
    "count": 2,
    "num": "47、43"
  },
  {
    "name": "上海科技大学",
    "longitude": 121.595394,
    "latitude": 31.177971,
    "count": 1,
    "num": "34"
  },
  {
    "name": "同济大学",
    "longitude": 121.500829,
    "latitude": 31.283599,
    "count": 1,
    "num": "11"
  },
  {
    "name": "西安电子科技大学",
    "longitude": 108.916313,
    "latitude": 34.231646,
    "count": 2,
    "num": "27、38"
  },
  {
    "name": "西安交通大学",
    "longitude": 108.983166,
    "latitude": 34.247359,
    "count": 8,
    "num": "28、12、17、23、29、33、42、49"
  },
  {
    "name": "西北工业大学",
    "longitude": 108.9166507,
    "latitude": 34.243345,
    "count": 2,
    "num": "35、40"
  },
  {
    "name": "浙江大学",
    "longitude": 120.084406,
    "latitude": 30.303304,
    "count": 3,
    "num": "26、30、50"
  },
  {
    "name": "中国科学技术大学",
    "longitude": 117.270137,
    "latitude": 31.837919,
    "count": 1,
    "num": "39"
  },
  {
    "name": "中国人民大学",
    "longitude": 116.312769,
    "latitude": 39.970546,
    "count": 2,
    "num": "29、52"
  },
  {
    "name": "中央财经大学",
    "longitude": 116.342063,
    "latitude": 39.959211,
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
  margin-top: -10px;
  margin-bottom: 0px;
}
</style>
