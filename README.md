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
    FilterSearch,
  },
  data() {
    return {
      selectedApi: "",
      show: false,
      products: [
        { id: "p1", name: "teclado", precio: 50, calidad: 8, popularidad: 7 },
        { id: "p2", name: "ratón", precio: 40, calidad: 7, popularidad: 9 },
        { id: "p3", name: "monitor", precio: 150, calidad: 9, popularidad: 6 },
      ],
      productFilter: [],
      clients: [
        {
          id: "c1",
          name: "cliente",
        },
      ],
    };
  },
  methods: {
    updateProducts(filteredOptions) {
      this.productFilter = filteredOptions;
    },
    updateClients(filteredOptions) {
      this.clients = filteredOptions;
    },
  },
};
```

### How to add it to our VUE structure?

```html
<template>
  <div class="parent-component">
    <div class="filter-component">
      <FilterSearch
        class="custom-button"
        label="Products"
        :filterOptions="products"
        @update="updateProducts"
      />
      <FilterSearch
        class="custom-button"
        label="Clients"
        :filterOptions="clients"
        @update="updateClients"
      />
    </div>
  </div>
</template>
```

## How is the information displayed?

```html
<div v-show="showResults" class="search-component__results">
        <p
          v-for="option in filteredOptions"
          :key="option.id"
          class="search-component__results-title"
        >
          {{ option.name }}
          <input
            class="search-component__results-checkbox"
            type="checkbox"
            v-model="option.checked"
          />
        </p>
      </div>
    </div>
```

### How to modify css?

```css
/* Father component */
.search-component {
  background-color: white;
  font-family: Ubuntu;
  align-items: center;
  border-radius: 5px;
  width: 150px;
  height: 150px;
  color: #333;
}
```
