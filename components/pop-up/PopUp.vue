<template>
  <div
    class="fixed top-0 left-0 w-full h-full flex items-center justify-center bg-black bg-opacity-70"
  >
    <div>
      <div v-if="isMobile">
        <MobileContent @close-popup="handleClosePopup" />
      </div>
      <div
        v-else
        class="fixed top-0 left-0 w-full h-full flex items-center justify-center"
      >
        <div class="relative w-11/12 h-5/6 bg-white">
          <button
            @click="handleClosePopup"
            class="absolute top-4 right-4 text-gray-400 text-2xl hover:text-gray-600"
          >
            <i class="fas fa-times"></i>
          </button>
          <div class="p-6 h-full overflow-y-auto">
            <!-- Tab buttons -->
            <div class="flex w-24 mb-4">
              <button
                @click="setActiveTab('images')"
                :class="{ 'bg-gray-300': activeTab === 'images' }"
                class="flex-1 px-2 py-1 text-center cursor-pointer hover:bg-gray-200"
              >
                Images
              </button>
              <button
                @click="setActiveTab('videos')"
                :class="{ 'bg-gray-300': activeTab === 'videos' }"
                class="flex-1 px-2 py-1 text-center cursor-pointer hover:bg-gray-200"
              >
                Videos
              </button>
            </div>
            <div class="border-b-2 border-gray-300 mb-4"></div>

            <!-- Tab content -->
            <div v-if="activeTab === 'images'">
              <Images />
            </div>
            <div v-else-if="activeTab === 'videos'">
              <Videos />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Images from "./Images.vue";
import Videos from "./Videos.vue";
import MobileContent from "./MobileContent.vue";

export default {
  name: "PopUp",
  components: {
    Images,
    Videos,
    MobileContent,
  },
  props: {
    closePopup: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      activeTab: "images",
      isMobile: false,
    };
  },
  mounted() {
    // Check the screen width on component mount and when the window is resized
    this.checkScreenWidth();
    window.addEventListener("resize", this.checkScreenWidth);
  },
  beforeDestroy() {
    // Remove the resize event listener when the component is destroyed
    window.removeEventListener("resize", this.checkScreenWidth);
  },
  methods: {
    handleClosePopup() {
      this.closePopup();
    },
    setActiveTab(tab) {
      this.activeTab = tab;
    },
    checkScreenWidth() {
      this.isMobile = window.innerWidth <= 768; // Adjust the breakpoint as needed
    },
  },
};
</script>
