<template>
  <div class="parent-component">
    <div class="filter-component">
      <FilterSearch
        class="custom-button"
        :filterOptions="products"
        @update="updateProducts"
      />
      <!-- <FilterSearch
        class="custom-button"
        :filterOptions="clients"
        @update="updateClients"
      /> -->
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
      products: [{
        label: 'Productos',
        options: [
        { code: "p1", label: "teclado"},
        { code: "p2", label: "ratón" },
        { code: "p3", label: "monitor" },
        { code: "p4", label: "cámara" },
        { code: "p5", label: "altavoz" },
        { code: "p6", label: "auriculares" },
        { code: "p7", label: "impresora" },
        { code: "p8", label: "escáner" },
        { code: "p9", label: "disco duro" },
        { code: "p10", label: "procesador" },
        ]}],
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
</script>

<style scoped>
.parent-component {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.filter-component {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-bottom: 20px;
}

.custom-button {
  font-size: 15px;
  border-radius: 5px;
  margin-right: 10px;
  margin-bottom: 10px;
  margin-left: 50px;
}
</style>
