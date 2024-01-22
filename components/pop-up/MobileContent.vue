<template>
  <div
    class="w-full h-screen flex flex-col bg-white p-4"
    ref="mobileContentWrapper"
  >
    <div
      class="flex-1 flex flex-col justify-center items-center overflow-hidden"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <img
        v-if="selectedItem && selectedItem.normal"
        :key="'img-' + selectedItem.id"
        :src="selectedItem.normal"
        :alt="'Selected Item ' + selectedItem.id"
        class="w-full h-full object-fill"
      />
      <video
        v-else-if="selectedItem && selectedItem.normalVideo"
        :key="'video-' + selectedItem.id"
        :src="selectedItem.normalVideo"
        controls
        class="w-full h-full object-cover"
      ></video>
    </div>

    <!-- Thumbnail section -->
    <div class="flex gap-2 mt-4 px-4">
      <img
        v-for="item in mobileContent"
        :key="'thumbnail-' + item.id"
        :src="item.thumbnail"
        :alt="'Thumbnail ' + item.id"
        @click="handleSelectItem(item)"
        class="w-12 h-12 cursor-pointer border border-gray-400"
      />
    </div>
  </div>
</template>

<script>
import { MobileContentData } from "../../data/data";

export default {
  name: "MobileContent",
  data() {
    return {
      mobileContent: MobileContentData,
      selectedItem: MobileContentData[0],
      touchStartX: 0,
      touchEndX: 0,
    };
  },
  methods: {
    handleSelectItem(item) {
      this.selectedItem = item;
    },
    handleSelectItem(item) {
      this.selectedItem = item;
    },
    handleTouchStart(event) {
      this.touchStartX = event.touches[0].clientX;
    },
    handleTouchMove(event) {
      this.touchEndX = event.touches[0].clientX;
    },
    handleTouchEnd() {
      const touchThreshold = 50;

      if (this.touchStartX - this.touchEndX > touchThreshold) {
        this.showNextItem();
      } else if (this.touchEndX - this.touchStartX > touchThreshold) {
        this.showPreviousItem();
      }
    },
    showNextItem() {
      const currentIndex = this.mobileContent.indexOf(this.selectedItem);
      const nextIndex = (currentIndex + 1) % this.mobileContent.length;
      this.selectedItem = this.mobileContent[nextIndex];
    },
    showPreviousItem() {
      const currentIndex = this.mobileContent.indexOf(this.selectedItem);
      const previousIndex =
        (currentIndex - 1 + this.mobileContent.length) %
        this.mobileContent.length;
      this.selectedItem = this.mobileContent[previousIndex];
    },
  },
};
</script>

<style scoped>
.carousel-item img,
.carousel-item video {
  border: 2px solid transparent;
}

.carousel-item img[selected],
.carousel-item video[selected] {
  border: 2px solid blue;
}
</style>
