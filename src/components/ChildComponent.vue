<template>
  <div class="parent-component">

    <div class="filter-component">
      <FilterSearch label="Products" :filterOptions="products" />
      <FilterSearch label="Clients" :filterOptions="clients" />
    </div>
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
      show: false,
      products: [{
        id: 'p1',
        name: 'product'
      },
    {
      id: 'p2',
        name: 'teclado'
    }],
      clients: [{
        id: 'c1',
        name: 'cliente'
      },
    {
      id: 'c2',
        name: 'eladio'
    }]
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

.button-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px; 
}

.custom-button {
  font-size: 15px;
  border-radius: 5px; /* Aplica el mismo borde redondeado que el input */
  margin-right: 10px;
  margin-bottom: 10px;
  padding: 8px 16px; /* Ajusta el relleno según sea necesario */
  border: 2px solid #ccc;
  outline: none;
  transition: border-color 0.3s ease;
}

.filter-component {
  width: 100px;
  height: 200px;
  margin: 0 auto; 
  margin-top: 15px;
  display: flex;
  flex-direction: row; 
  justify-content: space-around;
  align-items: center; 
}

button {
  font-size: 15px;
}
</style>