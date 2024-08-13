<!-- App.vue -->
<template>
  <div id="app">
    <h1>Full Screen Image Gallery Demo</h1>
    <FullScreenImageGallery :images="imageUrls"/>
  </div>
</template>

<script>
import {ref} from 'vue'
import FullScreenImageGallery from './components/Viewer.vue'

export default {
  name: 'App',
  components: {
    FullScreenImageGallery
  },
  setup() {
    const imageUrls = ref([
      'https://cdn.pixabay.com/photo/2024/07/08/05/41/girl-8880144_960_720.png',
      'https://cdn.pixabay.com/photo/2024/07/25/09/52/farmer-8920644_960_720.jpg',
      'https://img.freepik.com/free-photo/aerial-beautiful-shot-seashore-with-hills-background-sunset_181624-24143.jpg?w=1800&t=st=1723531850~exp=1723532450~hmac=695a949488f964b3fca65251a76a0dc01d708982b605899b15be0ccce06b1836',
      'https://wallpapers.com/images/high/pinkish-sunset-in-new-york-iphone-u2lh1sr3m91pg2cv.webp',
      'https://www.shutterstock.com/image-vector/cargo-container-shipping-strength-shipment-260nw-446949145.jpg',
      // Add more image URLs as needed
      'https://as2.ftcdn.net/v2/jpg/04/19/75/85/1000_F_419758574_oaS4kKwAPdYOG6XDtonfy26QPjtDA1Wp.jpg'
    ])

    return {
      imageUrls
    }
  }
}
</script>