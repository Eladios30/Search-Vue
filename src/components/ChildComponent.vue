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
        { id: "p1", name: "teclado" },
        { id: "p2", name: "ratón" },
        { id: "p3", name: "monitor" },
        { id: "p4", name: "cámara" },
        { id: "p5", name: "altavoz" },
        { id: "p6", name: "auriculares" },
        { id: "p7", name: "impresora" },
        { id: "p8", name: "escáner" },
        { id: "p9", name: "disco duro" },
        { id: "p10", name: "procesador" },
      ],
      producstFilter: {

      },
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
      console.log('component filtrado');
      this.producstFilter = filteredOptions;
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
