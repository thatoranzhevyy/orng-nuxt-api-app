<template>
  <div class="max-w-screen-2xl mx-auto px-4 py-4 relative">
    <div class="columns-4 gap-1 [&>img:not(:first-child)]:mt-1">
      <template v-for="artwork in artworks">
        <template v-for="asset in artwork.assets">
          <img :src="asset.image_url"/>
        </template>
      </template>
      <div v-if="pending">Loading...</div>
      <button @click="loadMore()">Load more</button>
    </div>
  </div>
</template>

<script setup>
const page = ref(1);
const lastPage = ref(1);
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

  $fetch(`https://orng.buhe.su/api/artwork`, {
    method: 'GET',
    params: {
      page: page.value
    }
  }).then(function (artworks) {
    appendArtworks(artworks.data);
    pending.value = false;
    lastPage.value = artworks.last_page;
  });
}

const appendArtworks = (newArtworks) => {
  newArtworks.forEach((artwork) => {
    artworks.value.push(artwork);
  });
}
</script>