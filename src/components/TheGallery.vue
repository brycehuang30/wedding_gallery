<template>
<div class="gallery-container">

  <div class="gallery">
    <div v-for="(photo, index) in photos" :key="index" class="gallery-item">
      <figure>
        <img :src="photo.sm" />

        
        <!-- <figcaption>Picture of a few dogs having a rest and sleeping.</figcaption> -->
      </figure>
    <!-- <p>OMG, seriously how cute are these dogs?</p> -->
    </div>
  </div>
</div>
</template>

<script lang="ts">

interface Photo {
  sm: string,
  lg: string,
}

export default {
  data() {
    return {
      photos: [] as Photo[],
    }
  },
  mounted() {
    for(let i = 1; i <= 50; i++) {
      this.photos.push(
        {
          sm: new URL(`../assets/gallery-photos/${i}_sm.jpg`, import.meta.url).toString(),
          lg: new URL(`../assets/gallery-photos/${i}.jpg`, import.meta.url).toString()
        }
      )
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