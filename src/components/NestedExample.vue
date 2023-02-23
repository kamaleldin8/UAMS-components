<template>
    <div class="row">
      <div class="col-8">
        <h3>Nested draggable</h3>
        <nested :tasks="list" />
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
    data() {
      return {
        list: [
  {
    "name": "Admin",
    "tasks": [
      {
        "name": "People",
        "tasks": [
          {
            "name": "Providers"
          },
          {
            "name": "Users",
            "tasks":[
              {
                "name":"Manage Users",
                "tasks":[
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
        "tasks":[
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
  