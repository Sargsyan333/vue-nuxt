<template>
  <div class="relative">
    <div class="flex w-full justify-center items-center">
      <video
        :key="currentVideo.id"
        :src="currentVideo.image"
        :alt="'Video ' + currentVideo.id"
        class="w-screen h-full object-cover"
        controls
        autoplay
        muted
        loop
      ></video>
    </div>
    <button
      @click="nextVideo"
      class="absolute top-1/2 right-4 transform -translate-y-1/2 text-white bg-blue-800 rounded-full p-2 hover:bg-blue-600"
    >
      <i class="fas fa-chevron-right"></i>
    </button>
  </div>
</template>

<script>
import { carouselVideos } from "../../data/data";
import "@fortawesome/fontawesome-free/css/all.css";

export default {
  data() {
    return {
      currentVideoIndex: 0,
      carouselVideos: carouselVideos || [],
    };
  },
  computed: {
    currentVideo() {
      return this.carouselVideos[this.currentVideoIndex];
    },
  },
  methods: {
    nextVideo() {
      this.currentVideoIndex =
        (this.currentVideoIndex + 1) % this.carouselVideos.length;
    },
  },
  created() {
    this.carouselVideos = carouselVideos || [];
    console.log("Carousel Videos:", this.carouselVideos);
  },
};
</script>
