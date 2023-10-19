<template>
  <div class="filter-component">

    <button @click="handleApiSelection('posts')">API 1</button>
    <button @click="handleApiSelection('photos')">API 2</button>

    <FilterSearch :apiQuery="selectedApi" />
  </div>
</template>

<script>
import FilterSearch from './FilterSearch.vue';
export default {
  components: {
    FilterSearch
  },
  data() {
    return {
      selectedApi: '',
    };
  },
  methods: {
    handleApiSelection(param) {
      let url = `https://jsonplaceholder.typicode.com/${param}/?_limit=12`;
      this.selectedApi = url;
    },
  }
};
</script>
