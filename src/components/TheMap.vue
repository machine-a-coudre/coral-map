<script setup lang="ts">
import type { Coordinate } from '@geospatial-sdk/core/lib/model'
import { createMapFromContext } from '@geospatial-sdk/openlayers'
import TileLayer from 'ol/layer/Tile'
import OSM from 'ol/source/OSM.js'
import { onMounted, ref } from 'vue'

const mapContext = {
    layers: [
      {
        type: 'xyz',
        url: 'https://tile.openstreetmap.org/{z}/{x}/{y}.png'
      }
    ],
    view: {
        center: [0, 0] as Coordinate,
        zoom: 2
    }
}
const map = createMapFromContext(mapContext)
const mapRef = ref<HTMLElement | undefined>(undefined)

// map.addLayer(new TileLayer({
//       source: new OSM(),
//     }))

onMounted(() => {
  map?.setTarget(mapRef.value);
})
</script>

<template>
    <div ref="mapRef" style="height: 600px; width: 600px">
      <slot></slot>
    </div>
  </template>