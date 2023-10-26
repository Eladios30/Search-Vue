<template>
  <div class="parent-component">
    <div class="filter-component">
      <FilterSearch
        class="custom-button"
        label="Products"
        :filterOptions="products"
        @update="productFilter"
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
        { id: "p1", name: "teclado", precio: 50, calidad: 8, popularidad: 7 },
        { id: "p2", name: "ratón", precio: 40, calidad: 7, popularidad: 9 },
        { id: "p3", name: "monitor", precio: 150, calidad: 9, popularidad: 6 },
        { id: "p4", name: "cámara", precio: 100, calidad: 6, popularidad: 8 },
        { id: "p5", name: "altavoz", precio: 30, calidad: 7, popularidad: 7 },
        { id: "p6", name: "auriculares", precio: 20, calidad: 8, popularidad: 6,},
        { id: "p7", name: "impresora", precio: 80, calidad: 6, popularidad: 8 },
        { id: "p8", name: "escáner", precio: 70, calidad: 7, popularidad: 7 },
        { id: "p9", name: "disco duro", precio: 60, calidad: 8, popularidad: 6, },
        { id: "p10", name: "procesador", precio: 200, calidad: 9, popularidad: 5, },
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
      console.log("component filtrado");
      this.productFilter = filteredOptions;
    },
    updateClients(filteredOptions) {
      console.log(filteredOptions);
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
