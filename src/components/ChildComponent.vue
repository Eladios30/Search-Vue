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
