<script setup>
import Container from "./components/Container.vue";
</script>

<template>
  <div class="min-h-screen">
    <Container>
      <!-- Nav Bar -->
      <nav class="flex justify-between items-center w-full py-2 px-6 shadow-md">
        <div class="text-xl font-bold">
          <router-link to="/" class="text-white hover:text-gray-400">
            🌎 GlobeZones</router-link
          >
        </div>
        <div class="space-x-4">
          <router-link to="/about" class="text-white hover:text-gray-400"
            >About</router-link
          >
        </div>
      </nav>

      <router-view></router-view>
    </Container>
  </div>
</template>

<style scoped>
body,
html {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
}

nav {
  background-color: #04152a;
}
</style>
