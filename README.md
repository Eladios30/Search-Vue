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
      show: false,
      products: [
        {
          label: "Productos",
          options: [
            { code: "p1", label: "teclado" },
            { code: "p2", label: "ratón" },
            { code: "p3", label: "monitor" },
            { code: "p4", label: "cámara" },
            { code: "p5", label: "altavoz" },
            { code: "p6", label: "auriculares" },
            { code: "p7", label: "impresora" },
            { code: "p8", label: "escáner" },
            { code: "p9", label: "disco duro" },
            { code: "p10", label: "procesador" },
          ],
        },
        {
          label: "Clientes",
          options: [
            { code: "c1", label: "Electrónicos" },
            { code: "c2", label: "Ropa" },
            { code: "c3", label: "Accesorios" },
          ],
        },
        {
          label: "Estados",
          options: [
            { code: "e1", label: "Activo" },
            { code: "e2", label: "Inactivo" },
            { code: "e3", label: "En espera" },
            { code: "e4", label: "Finalizado" },
          ],
        },
        {
          label: "Videojuegos",
          options: [
            { code: "v1", label: "FIFA 2024" },
            { code: "v2", label: "Outlast" },
            { code: "v3", label: "Warzone 3" },
            { code: "v4", label: "Black Ops 2" },
            { code: "v5", label: "Battlefield" },
            { code: "v6", label: "Fortnite" },
          ],
        },
        {
          label: "Ropa",
          options: [
            { code: "r1", label: "Gucci" },
            { code: "r2", label: "Hugo Boss" },
            { code: "r3", label: "Zátillas" },
            { code: "r4", label: "Zapatos" },
            { code: "r5", label: "Pantalones de mezclilla" },
            { code: "r6", label: "Shorts" },
          ],
        },
      ],
    };
  },
};
```

### How to add it to our VUE structure?

```html
<FilterSearch
  class="parent-component__component"
  label="Productos"
  :filterOptions="products"
/>
<FilterSearch
  class="parent-component__component"
  label="Clientes"
  :filterOptions="products"
/>
<FilterSearch
  class="parent-component__component"
  label="Estados"
  :filterOptions="products"
/>
<FilterSearch
  class="parent-component__component"
  label="Videojuegos"
  :filterOptions="products"
/>
<FilterSearch
  class="parent-component__component"
  label="Ropa"
  :filterOptions="products"
/>
```

## How is the information displayed?

```html
<div v-show="showResults" class="search-component__results">
  <p
    v-for="option in filteredOptions"
    :key="option.code"
    class="search-component__results-title"
  >
    {{ option.code }} - {{ option.label }}
    <input
      class="search-component__results-checkbox"
      type="checkbox"
      v-model="option.checked"
    />
  </p>
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
