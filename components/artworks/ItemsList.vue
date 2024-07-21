<script>
import PhotoSwipeLightbox from 'photoswipe/lightbox';
import 'photoswipe/style.css';

export default {
  name: 'SimpleGallery',
  props: {
    galleryID: String,
    images: Array,
  },
  setup(props) {
    return {
      imagesData: props.images,
    };
  },
  mounted() {
    if (!this.lightbox) {
      this.lightbox = new PhotoSwipeLightbox({
        gallery: '#' + this.$props.galleryID,
        children: 'a',
        zoom: false,
        loop: false,
        bgOpacity: 1,
        pswpModule: () => import('photoswipe'),
      });
      this.lightbox.init();
    }
  },
  unmounted() {
    if (this.lightbox) {
      this.lightbox.destroy();
      this.lightbox = null;
    }
  },
  methods: {},
};
</script>

<template>
  <div :id="galleryID" class="flex flex-row flex-wrap gap-0.5">
    <a v-for="(image, key) in imagesData"
       :key="key"
       :href="image.image_url"
       :data-pswp-width="image.width"
       :data-pswp-height="image.height"
       target="_blank"
       rel="noreferrer"
       class="relative border-box overflow-hidden flex flex-auto items-center w-52 h-52">
      <img class="rounded absolute w-full h-full left-0 right-0 top-0 bottom-0 object-cover"
           :src="image.image_url">
    </a>
  </div>
</template>

<style scoped>

</style>
