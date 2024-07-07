<template>
  <div class="h-screen w-screen">
    <LMap
        ref="map"
        :zoom="zoom"
        :center="[43.2439296, 76.8966656]"
        :use-global-leaflet="false"
    >
      <LControl position="topleft">
        <UButton color="black" variant="solid" icon="i-heroicons-chevron-left" @click="$router.back()">
        </UButton>
      </LControl>
      <LTileLayer
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
          attribution="<a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a>"
          layer-type="base"
          name="OpenStreetMap"
      />
    </LMap>
  </div>
</template>

<script setup>
import {ref} from 'vue'

const zoom = ref(12)
</script>
