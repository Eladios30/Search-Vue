# Buscador or searcher

This is an advanced search engine that obtains information through an api that you pass and extracts it and displays it on the screen with manners and certain advanced structures.

## How to use it?
```js
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
    // Insert your own logic
    handleApiSelection(param) {
      let url = `https://jsonplaceholder.typicode.com/${param}/?_limit=12`; // api for example
      this.selectedApi = url;
    }
  }
};
```

### How to add it to our VUE structure?
```html
<template>
  <div class="filter-component">
    <!-- Button for example -->
    <button @click="handleApiSelection('posts')">API 1</button>
    <button @click="handleApiSelection('photos')">API 2</button>

    <FilterSearch :apiQuery="selectedApi" /> <!-- This is important! -->
  </div>
</template>
```

### How to modify css?
```css

```