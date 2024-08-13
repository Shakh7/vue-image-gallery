<template>
  <div>
    <div class="image-grid">
      <img
          v-for="(image, index) in images"
          :key="index"
          :src="image"
          @click="openFullScreen(index)"
          :alt="`Image ${index + 1}`"
          class="preview-image"
      />
    </div>
    <div v-if="isFullScreen" class="fullscreen-overlay" @click="closeFullScreen">
      <img :src="images[currentIndex]" :alt="`Full screen image ${currentIndex + 1}`" class="fullscreen-image"/>
      <div class="navigation">
        <button @click.stop="prevImage" class="nav-button">Previous</button>
        <button @click.stop="nextImage" class="nav-button">Next</button>
      </div>
      <div class="image-counter">{{ currentIndex + 1 }} / {{ images.length }}</div>
    </div>
  </div>
</template>

<script>
import {ref, computed} from 'vue'

export default {
  name: 'FullScreenImageGallery',
  props: {
    images: {
      type: Array,
      required: true
    }
  },
  setup(props) {
    const isFullScreen = ref(false)
    const currentIndex = ref(0)

    const openFullScreen = (index) => {
      currentIndex.value = index
      isFullScreen.value = true
    }

    const closeFullScreen = () => {
      isFullScreen.value = false
    }

    const nextImage = () => {
      currentIndex.value = (currentIndex.value + 1) % props.images.length
    }

    const prevImage = () => {
      currentIndex.value = (currentIndex.value - 1 + props.images.length) % props.images.length
    }

    return {
      isFullScreen,
      currentIndex,
      openFullScreen,
      closeFullScreen,
      nextImage,
      prevImage
    }
  }
}
</script>

<style scoped>
.image-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
}

.preview-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  cursor: pointer;
}

.fullscreen-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.9);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.fullscreen-image {
  max-width: 90%;
  max-height: 90%;
  object-fit: contain;
}

.navigation {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 20px;
}

.nav-button {
  padding: 10px 20px;
  background-color: rgba(255, 255, 255, 0.2);
  color: white;
  border: none;
  cursor: pointer;
}

.image-counter {
  position: absolute;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  color: white;
  font-size: 18px;
}
</style>