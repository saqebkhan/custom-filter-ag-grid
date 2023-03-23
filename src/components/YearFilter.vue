<template>
  <div>
    <div class="custom-filter">
      <input type="text" placeholder="Search" v-model="searchInput" />
      <hr />
      <div class="filter-options-container">
        <input
          type="checkbox"
          value="Select All"
          @change="onSelectAllChange"
          :checked="isAllSelected"
        />
        Select All
      </div>
      <div
        v-for="(option, index) in filteredFilterOptions"
        :key="index"
        style="padding: 2px"
      >
        <input
          type="checkbox"
          :value="option"
          v-model="selectedOptions"
          @change="onFilterChange"
        />
        {{ option }}
      </div>
    </div>
    <div class="filter-buttons">
      <button @click="resetFilters">Reset</button>
      <button @click="applyFilters">Apply</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomFilter",
  data() {
    return {
      selectedOptions: ["Alice", "Bob", "Daisy"],
      searchInput: "",
      filterOptions: ["Alice", "Bob", "Daisy"],
    };
  },
  computed: {
    isAllSelected() {
      return this.selectedOptions.length === this.filterOptions.length;
    },
    filteredFilterOptions() {
      return this.filterOptions.filter((option) =>
        option.toLowerCase().includes(this.searchInput.toLowerCase())
      );
    },
  },
  methods: {
    isFilterActive() {
      return this.selectedOptions.length > 0;
    },
    doesFilterPass(params) {
      return this.selectedOptions.includes(params.data.name);
    },
    getModel() {
      return { value: this.selectedOptions };
    },
    setModel(model) {
      this.selectedOptions = model ? model.value : [];
    },
    onFilterChange() {
      this.params.filterChangedCallback();
    },
    onSelectAllChange(event) {
      if (event.target.checked) {
        this.selectedOptions = [...this.filterOptions];
      } else {
        this.selectedOptions = [];
      }
      this.onFilterChange();
    },
    resetFilters() {
      this.selectedOptions = [];
      this.searchInput = "";
      this.params.filterChangedCallback();
    },
    applyFilters() {
      this.params.filterChangedCallback();
    },
  },
};
</script>

<style>
.custom-filter {
  max-height: 150px;
  overflow-y: auto;
  padding: 6px;
}
</style>
