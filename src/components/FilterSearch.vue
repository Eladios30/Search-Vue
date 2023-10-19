<template>
  <div :style="{ '--color-primary': primaryColor, '--color-secondary': secondaryColor, '--font-family': fontFamily, '--border-radius': borderRadius, '--width': width }" class="search-component">

    <!-- Modal para mostrar input -->
    <div v-if="show" class="search-component__modal">
      <div class="search-component__input-button">
        <input
        class="search-component__input"
        type="text"
        v-model="searchTerm"
        @input="filterPlaceholdersWithDelay"
        />
        <button class="search-component__selection-button" @click="applySelection">Aplicar Selección</button>
      </div>

      <div class="search-component__searchTerm" v-if="searchTerm.length >= 3">
        <div v-for="(placeholder, i) in filteredPlaceholders" :key="i" class="search-component__item">
          <input class="search-component__checkbox" type="checkbox" v-model="placeholder.selected" />
          <span class="search-component__title">{{ placeholder.title }}</span>
        </div>
      </div>
      <div v-else class="search-component__message">
        <span class="search-component__message-text">Ingrese más de 3 letras</span>
      </div>
    </div>

    <!-- Modal para mostrar los resultados -->
    <div class="search-component__modal search-component__result-modal" v-show="isModalVisible">
      <div class="search-component__modal-content">
        <span class="search-component__close-button" @click="closeModal">&times;</span>
        <span class="search-component__result-item" v-for="(selectedElement, index) in elementsSelect" :key="index">
          <p class="search-component__result-text">{{ selectedElement.id }} - {{ selectedElement.title }}</p>
        </span>
      </div>
    </div>

  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      placeholders: [],
      originalPlaceholders: [],
      elementsSelect: [],
      searchTerm: "",
      isModalVisible: false,
      show: true,
      searchTimeout: null,
    };
  },
  props: {
    apiQuery: {
      type: String,
      required: true,
    },
    primaryColor: {
      type: String,
      default: 'var(--color-primary)'
    },
    secondaryColor: {
      type: String,
      default: 'var(--color-secondary)'
    },
    fontFamily: {
      type: String,
      default: 'var(--font-family)'
    },
    borderRadius: {
      type: String,
      default: 'var(--border-radius)'
    },
    width: {
      type: String,
      default: 'var(--width)'
    }
  },
  computed: {
    filteredPlaceholders() {
      return this.placeholders.filter((placeholder) => {
        return placeholder.title
          .toLowerCase()
          .includes(this.searchTerm.toLowerCase());
      });
    },
    apiUrl(){
      return this.apiQuery;
    }
  },
  methods: {
    async fetchData(url) {
      try {
        const response = await axios.get(url);
        this.originalPlaceholders = response.data.map((item) => ({
          ...item,
          selected: false,
        }));
        this.placeholders = [...this.originalPlaceholders];
      } catch (error) {
        console.error(error);
      }
    },
    filterPlaceholdersWithDelay() {
      if (this.searchTimeout) {
        clearTimeout(this.searchTimeout);
      }

      this.searchTimeout = setTimeout(() => {
        if (this.searchTerm.length >= 3) {
          this.$emit("reset-placeholders");
        }
      }, 300);
    },

    applySelection() {
      if (this.elementsSelect.length > 0) {
        this.isModalVisible = true;
      }

      const selectedElements = this.filteredPlaceholders.filter(
        (placeholder) => placeholder.selected
      );

      this.elementsSelect.push(...selectedElements);

      this.isModalVisible = true;
    },
    openModal(){
      this.show = !this.show;
    },
    closeModal(){
      this.isModalVisible = false;
    }
  },
  watch: {
    apiUrl(){
      console.log(this.apiUrl)
      this.fetchData(this.apiUrl)
    },
    searchTerm() {
      this.filterPlaceholdersWithDelay();
    },
  },
};
</script>

<style scoped>
  :root {
    --color-primary: #28b761;
    --color-secundary: #6c757d;
    --font-family: Ubuntu, sans-serift;
    --border-radius: 4px;
    --width: 500px;
  }

  .search-component {
    background-color: var(--color-primary);
    color: black;
    border-radius: var(--border-radius);
    font-family: var(--font-family);
    width: var(--width);
  }

  .search-component__button {
    border-radius: 10px;
    margin-right: 10px;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, .2);
    font-size: 15px;
    margin-bottom: 10px;
  }

  .search-component__button:hover {
    background-color:  #bad6ff;
  }

  .search-component__input {
    border-radius: 4px;
    margin-right: 10px;
    margin-bottom: 10px;
  }

  .search-component__selection-button {
    border-radius: 10px;
    margin-right: 10px;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, .2);
    font-size: 15px;
    margin-bottom: 10px;
  }

  .search-component__selection-button:hover {
    background-color: #ffe4ba;
  }

  /* Estilos para el checkbox y el span */
  .search-component__searchTern {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 15px;
  }

  .search-component__item {
    margin-top: 10px;
    margin-bottom: 10px;
    font-size: 20px;
    cursor: pointer;
  }

  .search-component__checkbox {
      margin-right: 10px;
      opacity: 0;
  }

  .search-component__item:hover .search-component__checkbox {
      opacity: 1;
  }

  .search-component__title {
      font-size: 16px;
      color: #333;
  }

  .search-component__checkbox:checked + .search-component__title {
      font-weight: bold;
  }

</style>