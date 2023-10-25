<template>
  <div class="parent-component">
    <div class="filter-component">
      <FilterSearch class="custom-button" label="Products" :filterOptions="products" />
      <FilterSearch class="custom-button" label="Clients" :filterOptions="clients" />
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
          id: "p1",
          name: "product",
        },
        {
          id: "p2",
          name: "teclado",
        },
        {
          id: "p3",
          name: "producto",
        },
      ],
      clients: [
        {
          id: "c1",
          name: "cliente",
        },
        {
          id: "c2",
          name: "eladio",
        },
      ],
    };
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
  margin-bottom: 20px; /* Añade un margen inferior para separar los componentes FilterSearch */
}

.custom-button {
  font-size: 15px;
  border-radius: 5px;
  margin-right: 10px;
  margin-bottom: 10px;
  margin-left: 50px;
}
</style>

