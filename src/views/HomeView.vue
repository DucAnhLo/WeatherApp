<template>
  <main class="container text-white">
      <div class=" pt-4 mb-8 relative">
        <input
        v-model="searchQuery"
        type="text" 
        placeholder="Search for a city or state"
        class="py-2 px-1 w-full bg-transparent border rounded-lg focus:border-weather-secondary focus:outline-none"
        >
      </div>
  </main>
</template>

<script setup>
import { ref } from 'vue';

const searchQuery = ref("")

</script>

