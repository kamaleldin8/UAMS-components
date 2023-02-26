<template>
    <div class="row">
      <div class="col-8">
        <nested :nodes="list" />
      </div>
  
      <rawDisplayer class="col-3" :value="list" title="List" />
    </div>
  </template>
  
  <script>
  import nested from "./nested.vue";
  export default {
    name: "nested-example",
    display: "Nested",
    order: 15,
    components: {
    nested
    },
    watch: {
    root: {
      deep: true,
      handler: function (newRoot) {
        console.log(newRoot);
      },
    },
  },
  methods: {
    nodeWasClicked(node) {
      alert(node.name);
    },
  },
    data() {
      return {
        list: [
  {
    "name": "Admin",
    "children": [
      {
        "name": "People",
        "children": [
          {
            "name": "Providers"
          },
          {
            "name": "Users",
            "children":[
              {
                "name":"Manage Users",
                "children":[
                  {"name":"General"},
                  {"name":"Identity"},
                  {"name":"Clinic"},
                  {"name":"SecurityRoles"}
                ]

              }
            ]
          }
        ]
      }]
    },
    {
      "name":"Calender", 
        "children":[
        {
          "name":"test file"
      
        }
      ]
    },
    {
      "name":"Requests"
    }
  ]
      };
    }
  };
  </script>
  <style scoped></style>
  