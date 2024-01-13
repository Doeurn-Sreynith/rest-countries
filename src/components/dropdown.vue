<template>
    <div class="flex items-center">
      <label for="sorting" class="w-[120px]">Short by</label>
      <select id="sorting"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        v-model="selectedSort"
        @change="changeValue"
      >
        <option value="def">default</option>
        <option value="hi">Asc</option>
        <option value="desc">Desc</option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    name: "DropDown",
    props: {
      selectedSort: String, // Add selectedSort prop
    },
    data() {
      return {
        // Initialize selectedSort as a data property
        selectedSort: "def",
      };
    },
    methods: {
      changeValue() {
        this.$emit("sort", this.selectedSort); // Use 'this.selectedSort' instead of 'selectedSort'
      },
    },
  };
  </script>
  