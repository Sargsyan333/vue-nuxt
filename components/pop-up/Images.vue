<template>
  <div class="flex">
    <!-- Left Section -->
    <div class="w-1/2" v-on:dblclick="toggleZoom">
      <img
        :src="zoomedImage || selectedImage"
        :alt="'Selected Image'"
        class="w-full mb-4"
        :class="{ zoomed: zoomed }"
      />
    </div>

    <!-- Right Section-->
    <div
      class="flex flex-col gap-4 border-2 border-gray-500 w-1/2 h-1/2 p-8 m-8"
    >
      <div class="flex flex-col">
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam dolor
          risus, tristique et auctor quis, aliquam quis odio
        </p>
        <p
          class="text-sm md:text-sm font-semibold text-gray-600/50 dark:text-gray-500/50 whitespace-nowrap"
        >
          Colour Name: Black
        </p>
      </div>

      <div class="w-1/2 p-4 flex gap-4">
        <template v-if="showThumbnailItems">
          <div
            v-for="item in thumbnailItems"
            :key="'thumbnail-item-' + item.id"
            @click="handleSelectImage(item)"
          >
            <img
              :src="item.thumbnailImage"
              :alt="'Thumbnail ' + item.id"
              class="w-12 h-12 mb-2 cursor-pointer border border-gray-400"
            />
          </div>
        </template>
        <template v-else>
          <div
            v-for="item in carouselItems"
            :key="'carousel-item-' + item.id"
            @click="handleSelectImage(item)"
          >
            <img
              :src="item.image"
              :alt="'Carousel ' + item.id"
              class="w-12 h-12 mb-2 cursor-pointer border border-gray-500"
            />
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Images",
  data() {
    return {
      allImages: [
        {
          id: 1,
          normal: require("@/assets/product-image.jpeg"),
          thumbnail: require("@/assets/product-image-thumbnail.jpeg"),
          large: require("@/assets/product-image-large.jpeg"),
        },
        {
          id: 2,
          normal: require("@/assets/product-image-front.jpeg"),
          thumbnail: require("@/assets/product-image-front-thumbnail.jpeg"),
          large: require("@/assets/product-image-front-large.jpeg"),
        },
        {
          id: 3,
          normal: require("@/assets/product-image-back.jpeg"),
          thumbnail: require("@/assets/product-image-back-thumbnail.jpeg"),
          large: require("@/assets/product-image-back-large.jpeg"),
        },
      ],
      carouselItems: [],
      thumbnailItems: [],
      selectedImage: "",
      zoomed: true,
      zoomedImage: null,
    };
  },

  created() {
    if (this.allImages && this.allImages.length > 0) {
      this.carouselItems = this.allImages;
      this.thumbnailItems = this.allImages.map((image) => ({
        id: image.id,
        thumbnailImage: image.thumbnail,
        large: image.large,
      }));
      this.selectedImage = this.allImages[0].normal;
    } else {
      console.error("No images found!");
    }
  },
  computed: {
    showThumbnailItems() {
      if (this.allImages && this.allImages.length > 0) {
        const selectedNormalId = this.allImages.find(
          (image) => image.normal === this.selectedImage
        )?.id;

        return this.thumbnailItems.some(
          (thumbnail) => thumbnail.id === selectedNormalId
        );
      }

      return false;
    },
  },
  methods: {
    handleSelectImage(clickedItem) {
      if (this.allImages && this.allImages.length > 0) {
        const selectedNormalImage = this.allImages.find(
          (image) => image.id === clickedItem.id
        )?.normal;

        this.selectedImage = selectedNormalImage || this.selectedImage;
      }
    },
    toggleZoom() {
      if (this.selectedImage) {
        const selectedImageObj = this.allImages.find(
          (image) => image.normal === this.selectedImage
        );
        console.log(selectedImageObj);
        if (selectedImageObj) {
          this.zoomed = !this.zoomed;
          this.zoomedImage = this.zoomed
            ? selectedImageObj.normal
            : selectedImageObj.large;
        }
      }
    },
  },
};
</script>

<style scoped>
.zoomed {
  cursor: zoom-in;
  max-height: 80vh;
  object-fit: contain;
}

.overlay {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  z-index: 999;
  pointer-events: none; /* Disable pointer events by default */
}

.zoomed .overlay {
  pointer-events: auto; /* Enable pointer events when zoomed in */
}
</style>
