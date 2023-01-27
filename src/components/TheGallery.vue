<template>
<div class="gallery-container">

  <div class="gallery">
    <div v-for="(photo, index) in preview_photos" :key="index" class="gallery-item" @click="() => onShowLightBox(index)">
      <figure>
        <img :src="photo" />
        
        <!-- <figcaption>Picture of a few dogs having a rest and sleeping.</figcaption> -->
      </figure>
    <!-- <p>OMG, seriously how cute are these dogs?</p> -->
    </div>

    <vue-easy-lightbox
      :visible="is_lightbox_visible_ref"
      :index="lightbox_index_ref"
      :imgs="large_photos"
      :moveDisabled="true"
      :minZoom="1"
      :maxZoom="1.5"
      @hide="onHideLightBox"
    >
      <toolbar></toolbar>
    </vue-easy-lightbox>
  </div>
</div>
</template>

<script lang="ts">
import VueEasyLightbox from 'vue-easy-lightbox'

export default {
  components: {
    VueEasyLightbox,
  },
  data() {
    return {
      preview_photos: [] as string[],
      large_photos: [] as string[],
      gallery_url: "https://storage.googleapis.com/wedding_gallery/gallery-photos",
      is_lightbox_visible_ref: false,
      lightbox_index_ref: 0,
    }
  },
  methods: {
    onShowLightBox(index: number) {
      this.is_lightbox_visible_ref = true;
      this.lightbox_index_ref = index;
    },

    onHideLightBox() {
      this.is_lightbox_visible_ref = false;
    },
  },
  mounted() {
    for (let i = 1; i <= 50; i++) {
      this.preview_photos.push(`${this.gallery_url}/${i}_sm.jpg`);
      this.large_photos.push(`${this.gallery_url}/${i}.jpg`);
    }
  }
}
</script>

<style scoped>

.gallery-container {
  margin: 2rem auto;
  height: 90vh;
  overflow: auto;
}

.gallery {
  max-width: 1200px;
  margin: 0 auto;
  column-count: 4;
  font-family: arial;
}
.gallery-item {
  cursor: pointer;
  break-inside: avoid;
  margin-bottom: 16px;
}
.gallery-item figure {
  margin: 0;
  position: relative;
}
.gallery-item figcaption {
  font-style: italic;
  padding: 8px;
  position: absolute;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  box-sizing: border-box;
  bottom: 3px;
  color: #fff;
  height: 30px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  border-radius: 0 0 14px 14px;
}
.gallery-item img {
  width: 100%;
  border-radius: 14px;
}
.gallery-item p {
  margin: 0;
  padding: 8px;
}

:deep(.vel-btns-wrapper) {
  width : 100%;
  height : 100%;
}
:deep(.toolbar-btn__rotate) {
  display: none;
}

@media screen and (max-width: 500px) {
  .gallery-container {
    overflow: unset;
    height: unset;
  }

  .gallery {
    column-count: 2;
  }
}
@media screen and (min-width: 501px) and (max-width: 700px) {
  .gallery-container {
    overflow: unset;
    height: unset;
  }

  .gallery {
    column-count: 2;
  }
}
@media screen and (min-width: 701px) and (max-width: 900px) {
  .gallery-container {
    overflow: unset;
    height: unset;
  }

  .gallery {
    column-count: 3;
  }
}

</style>