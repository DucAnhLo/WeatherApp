<template>
  <main class="container text-white">
      <div class=" pt-4 mb-8 relative">
        <input
        v-model="searchQuery"
        @input="getSearchResults"
        type="text" 
        placeholder="Search for a city or state"
        class="py-2 px-1 w-full bg-transparent border rounded-lg focus:border-weather-secondary focus:outline-none"
        />
        <ul class=" absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top[66]"
        v-if="mapboxSearchResults">
        <p v-if="searchError">Something went wrong, please try again.</p>
        <p v-if="!serviceError && mapboxSearchResults.length === 0">No results match your query, try a different term</p>
          <li v-for="searchResult in mapboxSearchResults" :key="searchResult.id" class="py-2 cursor-pointer"  @click="previewCity(searchResult)">
            {{ searchResult.place_name }}
          </li>
        </ul>
      </div>
  </main>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios'

const mapboxAPIKey = "pk.eyJ1IjoiZHVjYW5obG8iLCJhIjoiY2xsaWIwZHc1MWFuYjNnbzM4aHdyb3prNCJ9.ig-0-rNY6TYdC_nJI7sJ9w"
const searchQuery = ref("")
const queryTimeOut = ref(null)
const mapboxSearchResults = ref(null)
const searchError = ref(null)

const getSearchResults = () => {
  clearTimeout(queryTimeOut.value);
  queryTimeOut.value = setTimeout(async () => {
    if(searchQuery.value !== ""){
      try {
        const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIKey}&types=place`);
        mapboxSearchResults.value = result.data.features;
      }
      catch {
        searchError.value = true
      }
      return;
    }
    mapboxSearchResults.value = null;
  }, 300)
}
</script>

