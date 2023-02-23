<template>
    <div class="row">
      <div class="col-8">
        <h3>Nested draggable</h3>
      </div>
  
      <!-- <rawDisplayer class="col-3" :value="list" title="List" /> -->
    </div>


    <div 
        v-for="node in nodes"
        :key="node.name"
        :style="{'margin-left': `${depth * 20}px`}" 
        class="node"
      >
        <span 
          class="type" 
          @click="nodeClicked(node)" 
        >
        <i v-if="isExpanded(node)" class="bi bi-chevron-down ">
          <i class="bi bi-folder2-open"></i> </i>
       
        
          <span v-else  >   
            <i v-if="node.children" class="bi bi-chevron-right"> <i  class="bi bi-folder"></i>   </i>   
            <i v-else class="bi bi-file-text" > </i>
          </span>

      </span>
        <span class="test"
         >{{node.name}}</span>
         <!-- :nodes="rootData" @onClick="nodeWasClicked" -->
        <!-- <dragcomp  
          v-if="isExpanded(node) && node.children"
          :nodes="node.children"
          :depth="depth + 1"
          @onClick="(node) => $emit('onClick', node)"
        /> -->
        <dragcomp :nodes="rootData"
       
        
        ></dragcomp>
        <!-- <rawDisplayer class="col-3" :value="list" title="List" /> -->

    </div>




  </template>
  
  <script>
  import dragcomp from "./Draggable-Component.vue";
  import root from '@/root.json'
  export default {
    name: "nested-example",
    display: "Nested",
    order: 15,
    components: {
   
      dragcomp
    },
    props: {
      nodes: Array,
      depth: {
        type: Number,
        default: 0,
      },
    },
    methods:{
      isExpanded(node) {
        return this.expanded.indexOf(node) !== -1;
      },
      nodeClicked(node) {
        
        this.active = true;

        if(node.children){
        
          if (!this.isExpanded(node)) {
          this.expanded.push(node);
        } else {
          this.expanded.splice(this.expanded.indexOf(node));

        }
        }
       
      },
        
    }
    ,
    data() {
      return {
        rootData:root,
        expanded: [],

        list: [
          {
            name: "task 1",
            tasks: [
              {
                name: "task 2",
                tasks: []
              }
            ]
          },
          {
            name: "task 3",
            tasks: [
              {
                name: "task 4",
                tasks: []
              }
            ]
          },
          {
            name: "task 5",
            tasks: []
          }
        ]
      };
    }
  };
  </script>
  <style scoped></style>
  