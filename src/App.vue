<template>
  <div>
    <ag-grid-vue
      style="width: 500px; height: 500px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
    ></ag-grid-vue>
  </div>
</template>

<script>
import { AgGridVue } from "ag-grid-vue3";
import YearFilter from "./components/YearFilter.vue";
import AgeFilter from "./components/AgeFilter.vue";
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
export default {
  components: {
    AgGridVue,
  },
  data() {
    return {
      columnDefs: [
        {
          headerName: "Name",
          field: "name",
          filterFramework: YearFilter,
        },
        {
          headerName: "Age",
          field: "age",
          filterFramework: AgeFilter,
        },
      ],
      rowData: [
        { name: "Alice", age: '16' },
        { name: "Bob", age: '12' },
        { name: "Daisy", age: '9' },
      ],
    };
  },
};
</script>

<style>

</style>
