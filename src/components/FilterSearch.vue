<template>
  <div
    :style="{
      '--color-primary': primaryColor,
      '--color-secondary': secondaryColor,
      '--font-family': fontFamily,
      '--border-radius': borderRadius,
      '--width': width,
    }"
    class="search-component"
  >
    <!-- Modal para mostrar input -->
    <div v-if="show" class="search-component__modal">
      <div class="search-component__input-button">
        <input
          class="search-component__input"
          type="text"
          v-model="searchTerm"
          @input="filterPlaceholdersWithDelay"
        />
        <button
          class="search-component__selection-button"
          @click="applySelection"
        >
          Aplicar Selección
        </button>
      </div>

      <div class="search-component__search-term" v-if="searchTerm.length >= 3">
        <div
          class="search-component__item"
          v-for="(placeholder, i) in filteredPlaceholders"
          :key="i"
        >
          <span
            class="search-component__title"
            @mouseover="showCheckbox(placeholder)"
            @mouseout="hideCheckbox(placeholder)"
            @click="toggleCheckbox(placeholder)"
            >{{ placeholder.title }}</span
          >
          <input
            class="search-component__checkbox"
            type="checkbox"
            v-model="placeholder.selected"
          />
        </div>
      </div>
      <div v-else class="search-component__message">
        <span class="search-component__message-text"
          >Ingrese más de 3 letras</span
        >
      </div>
    </div>

    <!-- Modal para mostrar los resultados -->
    <div class="search-component__result-modal" v-show="isModalVisible">
      <div class="search-component__modal-content">
        <button class="search-component__close-button" @click="closeModal">
          &times;
        </button>
        <span
          class="search-component__result-item"
          v-for="(selectedElement, index) in elementsSelect"
          :key="index"
        >
          <p class="search-component__result-text">
            {{ selectedElement.id }} - {{ selectedElement.title }}
          </p>
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
      default: "var(--color-primary)",
    },
    secondaryColor: {
      type: String,
      default: "var(--color-secondary)",
    },
    fontFamily: {
      type: String,
      default: "var(--font-family)",
    },
    borderRadius: {
      type: String,
      default: "var(--border-radius)",
    },
    width: {
      type: String,
      default: "var(--width)",
    },
  },
  computed: {
    filteredPlaceholders() {
      return this.placeholders.filter((placeholder) => {
        return placeholder.title
          .toLowerCase()
          .includes(this.searchTerm.toLowerCase());
      });
    },
    apiUrl() {
      return this.apiQuery;
    },
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
    openModal() {
      this.show = !this.show;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    showCheckbox(placeholder) {
      placeholder.showCheckbox = true;
    },
    hideCheckbox(placeholder) {
      placeholder.showCheckbox = false;
    },
    toggleCheckbox(placeholder) {
      placeholder.selected = !placeholder.selected;
    },
  },
  watch: {
    apiUrl() {
      this.fetchData(this.apiUrl);
    },
    searchTerm() {
      this.filterPlaceholdersWithDelay();
    },
  },
};
</script>

<style scoped lang="scss">
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

  &__input-button {
    margin-top: 15px;
    font-size: 15px;

    .search-component__input {
      border-radius: 5px;
      margin-right: 10px;
      margin-bottom: 10px;
      padding: 8px;
      border: 2px solid #ccc;
      border-radius: 5px;
      outline: none;
      transition: border-color 0.3s ease;

      &:focus {
        border-color: #3498db;
      }
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
    align-items: center;
    margin-top: 15px;

    .search-component__item {
      margin-top: 10px;
      margin-bottom: 10px;
      font-size: 19px;
      cursor: pointer;
    }

    .search-component__item, .search-component__title {
    &:hover + .search-component__checkbox,
    .search-component__checkbox:focus {
      opacity: 1;
      }
    }

    .search-component__checkbox {
      margin-left: 10px;
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

    .search-component__modal-content {
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
      text-align: center;
    }

    .search-component__close-button {
      background: none;
      font-size: 10px;
      padding: 10px;
      border: none;
      font-size: 50px;
      color: #ff4444;
      cursor: pointer;
      position: absolute;
      top: 10px;
      right: 10px;
    }

    .search-component__result-item {
      margin-top: 20px;
    }

    .search-component__result-text {
      font-size: 18px;
      color: #333;
      margin: 5px 0;
    }
  }
}
</style>
