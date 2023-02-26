<template>
  <h3>Draggable DataTree</h3>
  <NestedExample></NestedExample>
  <h3>Tabber</h3>
  <TabberComponent></TabberComponent>
  <h3>DataTable</h3>
  <DataTable></DataTable>
</template>

<script>
import NestedExample from "./components/NestedExample.vue";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap";
import "bootstrap-icons/font/bootstrap-icons.css";
import TabberComponent from "./components/TabberComponent.vue";
import DataTable from "./components/DataTable.vue";
import 'vue-good-table-next/dist/vue-good-table-next.css'



export default {
  data() {
    return {};
  },



  name: "App",
  components: {
    NestedExample,
    TabberComponent,
    DataTable,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
