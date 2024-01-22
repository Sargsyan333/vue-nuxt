<template>
  <div class="relative p-8">
    <button
      @click="prevSlide"
      class="absolute top-1/4 transform -translate-y-1/2 text-blue-800 hover:text-blue-600"
    >
      <i class="fas fa-chevron-left"></i>
    </button>
    <div class="flex w-full justify-center items-center">
      <img
        @click="openPopup"
        :src="currentItem.image"
        :alt="'Product ' + currentItem.id"
        class="mx-auto w-1/2 h-1/2"
      />
    </div>
    <button
      @click="nextSlide"
      class="absolute top-1/4 transform -translate-y-1/2 right-4 text-blue-800 hover:text-blue-600"
    >
      <i class="fas fa-chevron-right"></i>
    </button>

    <!-- Pagination -->
    <div class="flex justify-center mt-4">
      <input
        type="radio"
        v-for="(item, index) in carouselItems"
        :key="'radio' + item.id"
        :id="'radio' + index"
        :value="index"
        v-model="currentIndex"
        class="hidden"
        ref="paginationInput"
      />

      <label
        v-for="(item, index) in carouselItems"
        :key="'label' + item.id"
        :for="'radio' + index"
        class="w-4 h-4 mx-1 rounded-full bg-gray-300 cursor-pointer hover:bg-gray-400 transition"
        :class="{ 'bg-red-600': index === currentIndex }"
        ref="paginationLabel"
      ></label>
    </div>
    <PopUp v-if="showPopup" :closePopup="closePopupHandler" />
  </div>
</template>

<script>
import PopUp from "./pop-up/PopUp.vue";
import { carouselItems } from "../data/data";
import "@fortawesome/fontawesome-free/css/all.css";

export default {
  components: {
    PopUp,
  },
  data() {
    return {
      currentIndex: 0,
      showPopup: false,
      carouselItems,
    };
  },
  computed: {
    currentItem() {
      return this.carouselItems[this.currentIndex];
    },
  },
  methods: {
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.carouselItems.length;
    },
    prevSlide() {
      this.currentIndex =
        (this.currentIndex - 1 + this.carouselItems.length) %
        this.carouselItems.length;
    },
    openPopup() {
      this.showPopup = true;
    },
    closePopupHandler() {
      this.showPopup = false;
    },
  },
};
</script>
