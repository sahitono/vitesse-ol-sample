<script setup lang="ts">
import { Map as OlMap, View } from "ol"
import { transform } from "ol/proj"
import { XYZ } from "ol/source"
import TileLayer from "ol/layer/Tile"

const map = new OlMap({})

function goToLocation(longitude: number, latitude: number) {
  const [x, y] = transform([longitude, latitude], "EPSG:4326", "EPSG:3857")
  map.getView().animate({
    center: [x, y],
    zoom: 10,
  })

  console.log(longitude, latitude)
}

onMounted(() => {
  map.setView(new View({
    center: [117.2, -3.2],
    zoom: 5,
    projection: "EPSG:3857",
    enableRotation: false,
  }))

  map.addLayer(
    new TileLayer({
      source: new XYZ({
        url: "https://{1-4}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png",
        projection: "EPSG:3857",
        attributions: "© <a href=\"https://www.supermap.com/en-us/\" target=\"_blank\">SuperMap</a> 2022",
      }),
      preload: Infinity,
    }),
  )
  map.setTarget("map")

  console.log(map)
})
</script>

<template>
  <div class="absolute left-0 top-0 h-full w-full font-sans">
    <div class="relative w-1/4 z-10" style="left: 1rem; top: 5rem">
      <GoToLocationCard @go-to="goToLocation" />
    </div>
    <div id="map" class="map absolute h-full w-full left-0 top-0" />
  </div>
</template>

<style>
@import "ol/ol.css";
</style>
