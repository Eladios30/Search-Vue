<template>
  <div class="search-component">
    <button class="search-component__label" @click="openModal()">
      {{ label }}
    </button>

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
          class="search-component__results-title"
        >
          {{ option.name }}
          <input class="search-component__results-checkbox" type="checkbox" v-model="option.checked" />
        </p>
      </div>
    </div>

    <!-- Modal para mostrar resultados seleccionados -->
<div v-show="showResultsModal" class="search-component__modal-overlay">
  <div class="search-component__modal-content">
    <div class="search-component__modal-header">
      <h2>Resultados Seleccionados</h2>
      <button @click="closeModal">&times;</button>
    </div>
    <div class="search-component__selected-results">
      <p v-if="selectedOptions.length === 0">Ninguna opción seleccionada</p>
      <ul v-else>
        <li v-for="option in selectedOptions" :key="option.id">{{ option.id }}| {{ option.name }}</li>
      </ul>
    </div>
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
      showResultsModal: false,
      searchTimeout: null,
      selectedOptions: [],
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
    closeModal() {
      this.showResultsModal = false;
    },
    showModalResults() {
      if (this.searchTerm.length >= 3) {
        this.selectedOptions = this.filteredOptions.filter(
          option => option.checked
        );
        this.showResultsModal = true;
        this.searchTerm = '';
        this.filteredOptions.forEach(option => option.checked = false);
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
  align-items: center;
  border-radius: 5px;
  width: 150px;
  height: 150px;
  color: #333;

  &__label {
    background-color: transparent;
    border: 3px solid #ccc;
    color: black;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
    border-radius: 5px;
    transition: border-color 0.3s ease, color 0.3s ease;

    &:hover {
      border-color: #bbb;
    }

    &:active {
      border-color: #3498db;
      color: #3498db;
    }
  }

  &__input-button {
    position: relative;
    margin-top: 10px;
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
      font-size: 16px;
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

  &__results {
    display: block;
    margin-top: 20px;
    height: 100%;

    &-title {
      display: flex;
      align-items: center;
      cursor: pointer;

      .search-component__results-checkbox {
        margin-right: 10px;
        opacity: 0;
        transition: opacity 0.3s ease;
      }

      &:hover .search-component__results-checkbox {
        opacity: 1;
      }
    }
  }

  .search-component__input-container,
  .search-component__results,
  .search-component__results-title {
    width: 100%;
  }

  &__modal-overlay {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1000;
  }

  &__modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  &__modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;

    h2 {
      font-size: 18px;
    }

    button {
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
      color: #333;
    }
  }

}
</style>
