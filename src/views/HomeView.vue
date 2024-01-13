<template>

 <Popup @isClose="isVisible=false" :isVisible="isVisible" :data="popupData"  /> 
  <div class="w-full">
    <div class="w-full flex justify-between p-[4rem]">
      <div>
        <!-- Use DropDown component and pass selectedSort prop -->
        <Dropdown :selectedSort="selectedSort" @sort="handleSort" />
      </div>
      <div>
        <Search @change="handleSearch($event)" />
      </div>
    </div>
    
    <div
    class="w-full bg-gray-100 h-min-[50vh] p-[2rem] grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
    <div v-for="country in paginatedCountries" :key="country.name.common"
    class="max-w-sm rounded overflow-hidden shadow-lg bg-white">
    <img class="w-full h-[150px] object-contain hover:scale-[1.1] cursor-pointer duration-200 bg-gray-50" @click="showPopUp(country)" :src="country.flags.png"
    :alt="`Flag of ${country.name.common}`">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{ country.name.official }}</div>
      <div class="scroll_style h-[10rem] overflow-auto">
        <div  v-for="(name, codeLang) in country.name.nativeName" :key="name"  class="text-lg mb-2"><span class="font-semibold capitalize">{{ codeLang }}:</span> {{ name.official }}</div>
      </div>
      
    </div>
  </div>
</div>

<!-- Pagination Controls -->
<div class="w-full mt-4 flex justify-center items-center mb-4">
  <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="prevPage"
  :disabled="currentPage === 1">
  Previous
</button>
<span class="mx-4 text-lg font-semibold">
  Page {{ currentPage }} of {{ totalPages }}
</span>
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="nextPage"
:disabled="currentPage === totalPages">
Next
</button>
</div>
</div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Search from '@/components/search.vue';
import Dropdown from '@/components/dropdown.vue';
import Popup from '@/components/Popup.vue'
const countries = ref([]);
const itemsPerPage = 25; // Adjust the number of items per page as needed
const currentPage = ref(1);
const totalPages = ref(0);
const paginatedCountries = ref([]);
const isVisible=ref(false)
const popupData=ref()
const fetchData = async () => {
  try {
    const response = await fetch('https://restcountries.com/v3.1/all');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    countries.value = data;
    paginatedCountries.value = updatePagination(countries.value);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

const showPopUp=(data)=>{
  isVisible.value=true
  // console.log(data);
  popupData.value=data
}

const updatePagination = (data) => {
  // const tmp = [...data]
  totalPages.value = Math.ceil(data.length / itemsPerPage);
  const startIndex = (currentPage.value - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;
  const tmp = data.slice(startIndex, endIndex);
  return tmp
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
    paginatedCountries.value = updatePagination(countries.value);
  }
};

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
    paginatedCountries.value = updatePagination(countries.value);
  }
};

const handleSort = (selectedSort) => {
  // alert(selectedSort)
  const tmp = [...countries.value];
  
  if (selectedSort == 'hi') {
    // alert('hi')
    tmp.sort((a, b) => (a.name.official > b.name.official ? 1 : -1));
    
  } else if (selectedSort == "desc") {
    tmp.sort((a, b) => (a.name.official > b.name.official ? -1 : 1));
    
  }
  
  // Update the selectedSort in the parent component
  paginatedCountries.value = updatePagination(tmp);
}

const handleSearch = (searchTerm) => {
  paginatedCountries.value = updatePagination(
  countries.value.filter((country) => {
    const countryName = country.name.official.toLowerCase();
    if(countryName.includes(searchTerm.toLowerCase())){
      
      return country;
    }
  })
  );
  
 
};



onMounted(fetchData);
</script>

<style>
.scroll_style{
  
  &::-webkit-scrollbar {
    width: 5px;
    display: none;
    
    
  }
  &::-webkit-scrollbar-track{
    background: black;
    border-radius: 999px;
  }
  &::-webkit-scrollbar-thumb{
    background: #d6ccc2;
    border-radius: 999px;
  }
}
</style>