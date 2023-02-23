<template>
 <!-- <dragcomp 
     :nodes="rootData"
      @onClick="nodeWasClicked"></dragcomp> -->

<!-- <NestedDraggable></NestedDraggable> -->
<nested></nested>
<NestedExample></NestedExample>
</template>

<script>
// import  dragcomp from './components/Draggable-Component.vue';

// import NestedDraggable from './components/NestedDraggable.vue';

import nested from './components/nested.vue';
import NestedExample from './components/NestedExample.vue'
import "bootstrap/dist/css/bootstrap.min.css"
import "bootstrap"
import 'bootstrap-icons/font/bootstrap-icons.css';

export default {
  data(){return{
   
  }},
  
  watch: {
    root: {
      deep: true,
      handler:function(newRoot) {
        console.log(newRoot);
      },
    },
  },
  methods: {
    nodeWasClicked(node) {
      alert(node.name);
    },
  },
  
  name: 'App',
  components: {
   nested,NestedExample,
    // dragcomp,
// NestedDraggable 
 }
}
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
