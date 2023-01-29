<template>
  <div class="gallery-container">
    <div class="gallery">
      <div
        v-for="(photo, index) in preview_photos"
        :key="index"
        class="gallery-item"
        @click="() => onShowLightBox(index)"
      >
        <figure>
          <img :src="photo" />

          <!-- <figcaption>Picture of a few dogs having a rest and sleeping.</figcaption> -->
        </figure>
        <!-- <p>OMG, seriously how cute are these dogs?</p> -->
      </div>

      <div v-if="lightbox_visible" class="lightbox" @click="onHideLightBox">
        <div class="lighbox-image-wrapper">
          <img
            @click.prevent="() => {}"
            class="lighbox-image"
            :src="large_photos[lightbox_photo_index]"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      preview_photos: [] as string[],
      large_photos: [] as string[],
      gallery_url:
        "https://storage.googleapis.com/wedding_gallery/gallery-photos",
      lightbox_visible: false,
      lightbox_photo_index: 0,
    };
  },
  methods: {
    onShowLightBox(index: number) {
      this.lightbox_visible = true;
      this.lightbox_photo_index = index;
    },

    onHideLightBox() {
      this.lightbox_visible = false;
    },
    preloadImage(url: string): Promise<void> {
      return new Promise((resolve, reject) => {
        const preloadImg = new Image();
        preloadImg.onload = () => {
          resolve();
        };
        preloadImg.onerror = () => {
          reject(new Error(`Failed to load image from ${url}`));
        };
        preloadImg.src = url;
      });
    },
  },
  mounted() {
    for (let i = 1; i <= 50; i++) {
      this.preview_photos.push(`${this.gallery_url}/${i}_sm.jpg`);
      this.large_photos.push(`${this.gallery_url}/${i}.jpg`);

      this.large_photos.forEach((photo) => {
        this.preloadImage(photo);
      });
    }
  },
};
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

.lightbox {
  bottom: 0;
  left: 0;
  margin: 0;
  position: fixed;
  right: 0;
  top: 0;
  z-index: 9998;
  background-color: rgba(0, 0, 0, 0.5);
  transition: background-color 0.5s;
}

.lighbox-image-wrapper {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.lighbox-image {
  height: 90%;
  border-radius: 14px;
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
