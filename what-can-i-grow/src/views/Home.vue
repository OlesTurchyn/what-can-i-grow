<script setup>
import { ref } from "vue";
import InteractiveMap from "../components/InteractiveMap.vue";

const cardData = ref({
  name: "Welcome",
  temperatureRange: "Click on a zone to get started!",
});

function updateCard(data) {
  cardData.value = data;
}
</script>

<template>
  <div class="relative min-h-screen flex">
    <div class="w-3/5">
      <InteractiveMap />
    </div>
    <div class="w-2/5">
      <h3 class="text-lg mb-2 text-center p-2 font-sans">
        Explore the World's Plant Hardiness Zones
      </h3>
    </div>
  </div>
</template>

<style scoped>
.header-text {
  font-size: 2.5rem;
  font-weight: bold;
  color: #2d3748; /* Tailwind's gray-800 */
}
</style>
