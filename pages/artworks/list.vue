<script setup>

import PhotoSwipeLightbox from 'photoswipe/lightbox';
import 'photoswipe/style.css';

const page = ref(1);
const lastPage = ref(1);
const isLoaded = ref(false);
const artworks = ref([]);
const pending = ref(false);

onMounted(() => {
  loadArtworks();
})

const loadMore = () => {
  if (page.value + 1 <= lastPage.value) {
    page.value = page.value + 1;
    loadArtworks();
  }
}

const loadArtworks = () => {
  pending.value = true;
  const url = `https://orng.buhe.su/api/artwork`;
  // const url = 'http://localhost:8000/api/artwork';
  $fetch(url, {
    method: 'GET',
    params: {
      page: page.value
    }
  }).then(function (artworks) {
    appendArtworks(artworks.data);
    pending.value = false;
    isLoaded.value = true;
    lastPage.value = artworks.last_page;
  });
}

const appendArtworks = (newArtworks) => {
  newArtworks.forEach((artwork) => {
    artworks.value.push(artwork);
  });
}
</script>

<template>
  <div class="flex flex-col gap-4 p-4">
    <div v-for="artwork in artworks">
      <a class="py-2 flex items-center space-x-4" :href="artwork.artist.permalink" target="_blank">
        <UAvatar size="xl" :src="artwork.artist.large_avatar_url" :alt="artwork.artist.full_name"/>
        <div class="flex-auto">
          <div class="text-base text-slate-900 font-semibold dark:text-slate-300">{{ artwork.artist.full_name }}</div>
          <div>{{ artwork.artist.username }}</div>
        </div>
      </a>
      <div v-html='artwork.title+artwork.description_html'></div>
      <div class="flex flex-col rounded-xl">
        <artworks-items-list :galleryID="`gallery-list-${artwork.id}`" :images="artwork.assets"/>
      </div>
    </div>
    <u-button block label="Загрузить больше" @click="loadMore()" :loading="pending"/>
  </div>
</template>

<style scoped>

</style>