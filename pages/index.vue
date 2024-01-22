<template>
  <div class="md-flex-col">
    <Header />
    <div class="flex justify-between flex-col md:flex-row w-full h-full">
      <Carousels /> <Card />
    </div>
  </div>
</template>

<script>
import Card from "../components/Card.vue";
import Carousels from "../components/Carousels.vue";
import Header from "../components/Header.vue";

export default {
  name: "IndexPage",
  components: { Card, Header, Carousels },
};
</script>
