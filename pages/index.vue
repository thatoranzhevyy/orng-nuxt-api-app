<template>
  <div class="max-w-4xl mx-auto grid grid-cols-4 grid-rows-8 md:grid-rows-4 gap-4 p-4">
    <use-welcome/>
    <use-language/>
    <use-theme/>
    <use-memory/>
    <nuxt-link to="/maps" class="col-span-4 md:col-span-1 bg-purple-600 rounded-3xl">
      <img src="~/assets/google_maps_helpful_hero_1.width-1200.format-webp.webp"
           class="w-full rounded-3xl object-cover h-full">
    </nuxt-link>
    <use-artworks/>
    <use-battery/>
    <use-network/>
    <use-music/>
  </div>
</template>
