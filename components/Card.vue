<template>
  <div class="flex flex-col p-4 md:p-8 w-full md:w-1/2 gap-4">
    <div class="flex justify-between md:flex-nowrap">
      <p
        class="text-lg md:text-xl font-semibold text-gray-600/50 dark:text-gray-500/50 whitespace-nowrap"
      >
        SAMSUNG
      </p>
      <span
        class="text-sm md:text-base text-green-700 md:self-center whitespace-nowrap"
        >Hurry Limited Stock</span
      >
    </div>
    <p class="text-2xl font-bold">Samsung Galaxy S23 Plus 5G</p>
    <p class="text-2xl font-bold">€880.00</p>
    <div class="border-t-2 border-gray-500 my-2" />
    <div>
      <span class="font-bold">Sim:</span>
      <span>DUAL SIM</span>
    </div>
    <div>
      <span class="font-bold">Condition:</span>
      <span>LIKE NEW</span>
    </div>
    <div>
      <span class="font-bold">Colour:</span>
      <span>LAVENDER</span>
    </div>
    <div>
      <span class="font-bold">Network:</span>
      <span>UNLOCKED</span>
    </div>
    <div>
      <span class="font-bold">Storage:</span>
      <span>512GB</span>
    </div>
    <div class="border-t border-gray-500 my-2" />
    <div class="flex gap-4 items-center">
      <i class="fas fa-minus" @click="decrementCount"></i>
      <span>{{ count }}</span>
      <i class="fas fa-plus" @click="incrementCount"></i>
    </div>
    <button class="bg-yellow-400 p-2 text-xl font-medium rounded">
      Add to Basket
    </button>
  </div>
</template>

<script>
import "@fortawesome/fontawesome-free/css/all.css";

export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    incrementCount() {
      this.count++;
    },
    decrementCount() {
      if (this.count > 0) {
        this.count--;
      }
    },
  },
};
</script>

<style scoped>
body {
  font-family: "Lato", sans-serif;
}
</style>
