<template>
  <div class="custom-filter">
    <div>
      <input type="checkbox" value="Select All" @change="onSelectAllChange" :checked="isAllSelected" />
      Select All
    </div>
    <div v-for="option in filterOptions" :key="option">
      <input type="checkbox" :value="option" v-model="selectedOptions" @change="onFilterChange" />
      {{ option }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomFilter',
  data() {
    return {
      selectedOptions: [],
      filterOptions: ['Alice', 'Bob', 'Daisy'],
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
  },
};
</script>