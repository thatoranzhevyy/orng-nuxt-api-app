<script setup lang="ts">
const response = await fetch('https://orng.buhe.su/api/artwork')
const items = [];
const res = await response.json()
for (const datum of res.data) {
  items.push(datum.assets[0].image_url)
}
</script>

<template>
  <div class="col-span-4 md:col-span-2 row-span-2 bg-gray-100 dark:bg-gray-800 rounded-xl">
    <UCarousel
        v-slot="{ item }"
        :items="items"
        :ui="{ item: 'basis-full' }"
        class="rounded-lg overflow-hidden"
        arrows>
      <nuxt-link to="/artworks">
        <img :src="item" class="w-full object-cover h-96" draggable="false">
      </nuxt-link>
    </UCarousel>
  </div>
</template>
