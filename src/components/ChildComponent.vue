<template>
  <div class="parent-component">
    <div class="parent-component__filter-component">
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
    </div>
  </div>
</template>

<script>
import FilterSearch from "./FilterSearch.vue";
export default {
  components: {
    FilterSearch,
  },
  data() {
    return {
      selectedApi: "",
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
          label: "Categorías",
          options: [
            { code: "c1", label: "Electrónicos" },
            { code: "c2", label: "Ropa" },
            { code: "c3", label: "Accesorios" },
          ],
        },
      ],
      productFilter: [],
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
</script>

<style scoped lang="scss">
.parent-component {
  display: flex;
  justify-content: center;
  align-items: center;

  &__filter-component {
    display: flex;
    align-items: center;
  }
  .parent-component__component {
    margin-right: 60px;
  }
}
</style>
