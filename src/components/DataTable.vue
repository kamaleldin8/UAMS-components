<template>
  <!-- @on-selected-rows-change="selectionChanged" -->
  <h2>Our Good Table :)</h2>
  <div>
    <VueGoodTable
      :totalRows="totalRecords"
      v-on:selected-rows-change="selectionChanged"
      :columns="columns"
      :rows="rows"
      v-on:row-click="onRowClick"
      :select-options="{
        enabled: true,
        selectOnCheckboxOnly: true, // only select when checkbox is clicked instead of the row
        selectionInfoClass: 'custom-class',
        selectionText: 'rows selected',
        clearSelectionText: 'clear',
        disableSelectInfo: true, // disable the select info panel on top
        selectAllByGroup: true, // when used in combination with a grouped table, add a checkbox in the header row to check/uncheck the entire group
      }"
      :search-options="{
        enabled: true,
        // trigger: 'enter',
        // skipDiacritics: true,
        placeholder: 'Search this table',
      }"
      :pagination-options="{
        mode: 'remote',
        enabled: true,
        perPage: 10,
        position: 'top',
        perPageDropdown: [3, 7, 9],
      }"
    />
  </div>
</template>
    
    <script>
import { VueGoodTable } from "vue-good-table-next";

export default {
  name: "my-component",
  // add to component
  components: {
    VueGoodTable,
  },
  methods: {
    selectionChanged() {
      console.log(this.$refs["my-table"].selectedRows);
    },

    onRowClick(params) {
      console.log(params.row.name);
    },
  },

  data() {
    return {
      //records:[],
      rows: [],
      isLoading: false,
      totalRecords: 0,
      serverParams: {
        columnFilters: {},
        sort: {
          field: "",
          type: "",
        },
        // page: 1,
        // perPage: 5
      },

      columns: [
        {
          label: "albumId",
          field: "albumId",
        },
        {
          label: "title",
          field: "title",
          filterOptions: {
            styleClass: "class1", // class to be added to the parent th element
            enabled: true, // enable filter for this column
            placeholder: "Filter This Thing", // placeholder for filter input
            trigger: "enter",
            filterDropdownItems: [], // dropdown (with selected values) instead of text input
            filterFn: this.columnFilterFn, //custom filter function that
          },
          // type: "number",
        },

        {
          label: "id",
          field: "id",
          // type: "percentage",
        },
        {
          label: "thumbnailUrl",
          field: "thumbnailUrl",
        },
      ],
      //  rows:this.records
    };
  },
  beforeMount() {
    fetch("https://jsonplaceholder.typicode.com/photos", {})
      .then((res) => res.json())
      .then((data) => (this.rows = data))
      .then(console.log(typeof this.rows));
  },
};
</script>