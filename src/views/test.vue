<template>
    <div class="w-full">
      <div class="w-full flex justify-between p-[4rem]">
        <div class="">
          <Dropdown />
        </div>
        <div>
          <Search />
        </div>
      </div>
  
      <div class="w-full bg-gray-100 p-[2rem] grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
        <div v-for="country in paginatedCountries" :key="country.name.common"
          class="max-w-sm rounded overflow-hidden shadow-lg bg-white">
          <img class="w-full h-[150px] object-contain bg-gray-50" :src="country.flags.png" :alt="`Flag of ${country.name.common}`">
          <div class="px-6 py-4">
            <div class="font-bold text-xl mb-2">{{ country.name.official }}</div>
            <div v-for="(name, codeLang) in country.name.nativeName" :key="name" class="text-lg mb-2">
              <span class="font-semibold">{{ codeLang }}:</span> {{ name.official }}
            </div>
            <p class="text-gray-700 text-base"></p>
          </div>
        </div>
      </div>
  
      <!-- Pagination Controls -->
      <div class="w-full mt-4">
        <button @click="prevPage" :disabled="currentPage === 1">Previous</button>
        <span class="mx-4">Page {{ currentPage }} of {{ totalPages }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, watch } from 'vue';
  import Dropdown from '@/components/dropdown.vue';
  import Search from '@/components/search.vue';
  
  const countries = ref([
    // Your country data here (all 250 countries)
  ]);
  
  const itemsPerPage = 20; // Adjust the number of items per page as needed
  const currentPage = ref(1);
  const totalPages = ref(Math.ceil(countries.value.length / itemsPerPage));
  
  const paginatedCountries = ref([]);
  
  const updatePagination = () => {
    const startIndex = (currentPage.value - 1) * itemsPerPage;
    const endIndex = startIndex + itemsPerPage;
    paginatedCountries.value = countries.value.slice(startIndex, endIndex);
  };
  
  const prevPage = () => {
    if (currentPage.value > 1) {
      currentPage.value--;
      updatePagination();
    }
  };
  
  const nextPage = () => {
    if (currentPage.value < totalPages.value) {
      currentPage.value++;
      updatePagination();
    }
  };
  
  onMounted(updatePagination);
  watch(countries, updatePagination);
  </script>
  