<template>
  <div class="search-component">
    <button @click="openModal()">{{ label }}</button>

    <!-- Modal para mostrar input -->
    <div v-show="show" class="search-component__modal">
      <div class="search-component__input-button">
        <div class="search-component__input-container">
          <i class="fas fa-search search-component__icon"></i>
          <input
            class="search-component__input"
            type="text"
            v-model="searchTerm"
            @input="filterPlaceholdersWithDelay"
            placeholder="Buscar..."
          />
        </div>
        <button
          class="search-component__selection-button"
          v-if="searchTerm.length >= 3"
          @click="showModalResults"
        >
          Aplicar Selección
        </button>
        <p v-else>Write 3 or more letters</p>
      </div>

      <!-- Modal para resultados -->
      <div v-show="showResults" class="search-component__results">
        <p
          v-for="option in filteredOptions"
          :key="option.id"
          class="search-component__results__title"
        >
          {{ option.name }}
          <input type="checkbox" />
        </p>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";

export default {
  name: "FilterComponent",
  data() {
    return {
      searchTerm: "",
      show: false,
      showResults: false,
      searchTimeout: null,
    };
  },
  props: {
    label: String,
    filterOptions: Array,
  },
  computed: {
    filteredOptions() {
      const filtered = this.filterOptions.filter((option) =>
        option.name.toLowerCase().includes(this.searchTerm.toLowerCase())
      );
      console.log("Search Term:", this.searchTerm);
      console.log("Filtered Options:", filtered);
      return filtered;
    },
  },
  methods: {
    filterPlaceholdersWithDelay() {
      clearTimeout(this.searchTimeout);
      this.searchTimeout = setTimeout(() => {
        if (this.searchTerm.length >= 3) {
          this.showResults = true;
        } else {
          this.showResults = false;
        }
      }, 300);
    },
    openModal() {
      this.show = !this.show;
    },
    showModalResults() {
      if (this.searchTerm.length >= 3) {
        this.showResults = !this.showResults;
      }
    },
  },
  watch: {
    searchTerm() {
      this.filterPlaceholdersWithDelay();
    },
  },
};
</script>

<style scoped lang="scss">
.search-component {
  background-color: white;
  font-family: Ubuntu;
  margin-top: 15px;
  border-radius: 5px;
  width: 300px;
  height: 300px;
  color: #333;

  &__input-button {
    margin-top: 20px;
    font-size: 15px;

    .search-component__input-container {
      position: relative;
      display: inline-block;
    }

    .search-component__input {
      border-radius: 5px;
      margin-bottom: 10px;
      padding: 10px 30px 10px 40px;
      border: 2px solid #ffffff;
      border-radius: 5px;
      outline: none;
      transition: border-color 0.3s ease;
      font-size: 15px;
      width: 200px;

      &:focus {
        border-color: #3498db;
      }
    }

    .search-component__icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-90%) rotate(90deg);
      font-size: 16px; /* Tamaño del icono */
    }

    // Boton para aplicar seleccion
    .search-component__selection-button {
      padding: 10px 10px;
      background-color: #3498db;
      color: #ffffff;
      border: none;
      border-radius: 5px;
      transition: background-color 0.3s ease;

      &:hover {
        background-color: darken(#3498db, 10%);
      }
    }
  }

  // Cuadro de busqueda
  &__search-term {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-top: 15px;
    max-height: 250px;
    overflow-y: auto;
    border-radius: 5px;
    color: rgb(33, 33, 33);

    .search-component__item {
      margin-top: 0px;
      margin-bottom: 10px;
      font-size: 19px;
      cursor: pointer;
      display: block;
      align-items: center;
      border-radius: 5px;
      padding: 8px;
      width: 100%;
      text-align: left;

      &:nth-child(odd) {
        background-color: #f7f7f7;
      }
    }

    .search-component__title {
      margin-right: 10px;
      text-align: left;
    }

    .search-component__item,
    .search-component__title {
      &:hover + .search-component__checkbox,
      .search-component__checkbox:focus {
        opacity: 1;
      }
    }

    .search-component__checkbox {
      opacity: 0;
      transition: opacity 0.3s ease;
      width: 15px;
      height: 15px;
      transform: scale(1.5);
    }
  }

  // Modal del resultado
  &__result-modal {
    background-color: rgba(0, 0, 0, 0.8);
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2;
    overflow-y: auto;
  }

  .search-component__modal-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
    text-align: left;
    position: relative; /* Asegura que los elementos hijos se posicionen relativos a este contenedor */

    .search-component__close-button {
      background: none;
      font-size: 30px;
      border: none;
      color: black;
      cursor: pointer;
      position: absolute;
      margin: 5px;
      top: 0;
      right: 10px;
    }
  }

  .search-component__result-item {
    margin-top: 20px;
    text-align: left;
  }

  .search-component__result-text {
    font-size: 18px;
    color: #333;
    margin: 5px 0;
  }
}
</style>
