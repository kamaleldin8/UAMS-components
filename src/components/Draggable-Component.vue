<template>
    <div class="row">
      <div class="col-2">
        <div class="form-group">
          <div
            class="btn-group-vertical buttons"
            role="group"
            aria-label="Basic example"
          >
            <button class="btn btn-secondary" @click="add">Add</button>
            <button class="btn btn-secondary" @click="replace">Replace</button>
          </div>
        </div>
      </div>
  
      <div class="col-6">
        <!-- <h3>Draggable {{ draggingInfo }}</h3> -->
        <h3>Draggable </h3>

        <draggable
          :list="nodes"
          :disabled="!enabled"
          :group="{ name: 'g1' }"
          item-key="name"
          class="list-group"
          ghost-class="ghost"
          :move="checkMove"
          @start="dragging = true"
          @end="dragging = false"
        >

       

          <template #item="{ element }">
           <dragcomp  :nodes="element.nodes"></dragcomp>
          </template>
        </draggable>
      </div>
  
      <!-- <rawDisplayer class="col-3" :value="rootData" title="List" /> -->
    </div>
  </template>
  
  <script>
import draggable from "vuedraggable";
  let id = 1;
  export default {
  name:'dragcomp',
  
    order: 0,
    components: {
    draggable,
    
},
  props:{
    tasks: {
      required: true,
      type: Array
    }
  }
    ,
    data() {
      return {
        enabled: true,
        dragging: false
      };
    },
    // computed: {
    //   draggingInfo() {
    //     return this.dragging ? "under drag" : "";
    //   }
    // },
    methods: {
    
      add: function() {
        this.list.push({ name: "Juan " + id, id: id++ });
      },
      replace: function() {
        this.list = [{ name: "Edgard", id: id++ }];
      },
      checkMove: function(e) {
        window.console.log("Future index: " + e.draggedContext.futureIndex);
      }
    }
  };
  </script>
  <style scoped>
  .node {
    text-align: left;
    font-size: 18px;
    
  }
  
  .type {
    margin-right: 10px;
    /* color:blue; */
  }
 
  .buttons {
    margin-top: 35px;
  }
  .ghost {
    opacity: 0.5;
    background: #c8ebfb;
  }
  .not-draggable {
    cursor: no-drop;
  }
  </style>