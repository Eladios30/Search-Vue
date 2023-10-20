# Buscador or searcher

This is an advanced search engine that obtains information through an api that you pass and extracts it and displays it on the screen with manners and certain advanced structures.

## How install?
```bs
npm i buscador
```

## How to use it?
```js
export default {
  components: {
    FilterSearch
  },
  data() {
    return {
      selectedApi: '',
      show: false,
    };
  },
  methods: {
    // Insert your own logic
    handleApiSelection(param) {
      let url = `https://jsonplaceholder.typicode.com/${param}/?_limit=12`; // api for example
      this.selectedApi = url;
    },
    showFilter() {
      this.show = !this.show;
    }
  }
};
```

### How to add it to our VUE structure?
```html
<template>
  <div class="parent-component">
    <div class="button-container">
      <!-- Button for example -->
      <button class="custom-button" @click="handleApiSelection('posts'); showFilter()">Productos</button>
      <button class="custom-button" @click="handleApiSelection('photos'); showFilter()">Clientes</button>
    </div>

    <div class="filter-component">
      <!-- This is important! -->
      <FilterSearch :apiQuery="selectedApi" v-show="show"/>
    </div>
  </div>
</template>
```

## How is the information displayed?
```html
<div
  class="search-component__item"
  v-for="(placeholder, i) in filteredPlaceholders"
  :key="i">
  <span
    class="search-component__title"
    @mouseover="showCheckbox(placeholder)"
    @mouseout="hideCheckbox(placeholder)"
    @click="toggleCheckbox(placeholder)"
    >{{ placeholder.title }}</span>
  <input
    class="search-component__checkbox"
    type="checkbox"
    v-model="placeholder.selected"/>
</div>
```

### How to modify css?
```css
/* Father component */
.search-component {
  background-color: #f6f6f6;
  font-family: Ubuntu;
  margin-top: 15px;
  border-radius: 5px;
  width: 300px;
  height: 300px;
  color: #333;
}
```