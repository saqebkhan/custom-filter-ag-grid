<template>
  <div class="custom-filter">
    <div>
      <input
        type="checkbox"
        value="Select All"
        @change="onSelectAllChange"
        :checked="isAllSelected"
      />
      Select All
    </div>
    <div v-for="option in filterOptions" :key="option">
      <input
        type="checkbox"
        :value="option"
        v-model="selectedOptions"
        @change="onFilterChange"
      />
      {{ option }}
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomFilter",
  data() {
    return {
      selectedOptions: [],
      filterOptions: ["Below 10", "10-18", "18-25", "Above 25"],
    };
  },
  computed: {
    isAllSelected() {
      return this.selectedOptions.length === this.filterOptions.length;
    },
  },
  methods: {
    isFilterActive() {
      return this.selectedOptions.length > 0;
    },
    doesFilterPass(params) {
      if (this.selectedOptions.includes("Below 10") && params.data.age < 10) {
        return true;
      } else if (
        this.selectedOptions.includes("10-18") &&
        params.data.age >= 10 &&
        params.data.age < 18
      ) {
        return true;
      } else if (
        this.selectedOptions.includes("18-25") &&
        params.data.age >= 18 &&
        params.data.age < 25
      ) {
        return true;
      } else if (
        this.selectedOptions.includes("Above 25") &&
        params.data.age >= 25
      ) {
        return true;
      }

      return false;
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
  },
};
</script>
