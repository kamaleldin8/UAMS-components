<template>
    <!-- <p  ref="testref">helllo</p> -->
  <draggable
    class="node"
    tag="ul"
    :list="tasks"
    :group="{ name: 'g1' }"
    item-key="name"
  >
    <template #item="{ element }">
      <li>
        <div :id= element.name @click="nodeClicked(element)" class="item-container node_element">
          <div >
          <span class="pr-5"  >
            <i v-if="isExpanded(element)" class="bi bi-chevron-down">
              <i class="bi bi-folder2-open"></i>
            </i>

            <span v-else>
              <i v-if="element.tasks" class="bi bi-chevron-right">
                <i class="bi bi-folder"></i>
              </i>
              <i v-else class="p-1 bi bi-file-text"> </i>
            </span>
          </span>
          <span class="p-1">{{ element.name }}</span>
        </div>
          <div>
            <button class="icon_button">
            <i v-if="addable" class="bi bi-plus-lg"></i>
          </button>
          <button class="icon_button">
            <i v-if="viewable" class="bi bi-eye-fill"></i>
          </button>
          <button class="icon_button">
            <i v-if="editable" class="bi bi-pen-fill"></i>
          </button>
          <button class="icon_button">
            <i v-if="deletable" class="bi bi-trash3-fill"></i>
          </button>
        </div>
        </div>
        <!-- recursion -->

        <nested-draggable
          :tasks="element.tasks"
          v-if="isExpanded(element) && element.tasks"
          :nodes="element.tasks"
          :depth="depth + 1"
          @onClick="(element) => $emit('onClick', element)"
        />
      </li>
    </template>
  </draggable>
</template>
  <script>
import draggable from "vuedraggable";

export default {
  data() {
    return {
      expanded: [],
      viewable: true,
      editable: true,
      addable: true,
      deletable: true,
    };
  },
  props: {
    tasks: {
      required: true,
      type: Array,
    },
  },
  methods: {
    isExpanded(node) {
      return this.expanded.indexOf(node) !== -1;
    },
    nodeClicked(node) {
    let allElements = document.getElementsByClassName('node_element');
    for (var i = 0; i < allElements.length; i++) {
      allElements[i].style.backgroundColor="transparent";
    }
    let catched_node = document.getElementById(node.name);
    catched_node.style.backgroundColor = 'lightgray';
      this.active = true;

      if (node.tasks) {
        if (!this.isExpanded(node)) {
          this.expanded.push(node);
        } else {
          this.expanded.splice(this.expanded.indexOf(node));
        }
      }
    },
  },
  components: {
    draggable,
  },
  name: "nested-draggable",
};
</script>
  <style scoped>
.dragArea {
  min-height: 50px;
  outline: 1px dashed;
}
ul {
  list-style-type: none;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  /* padding-left: 0; */
}
li {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 5px;
}
.node {
  text-align: left;
  font-size: 18px;
}

.type {
  margin-right: 10px;
  /* color:blue; */
}

.icon_button{
  background-color: transparent;
  border: none;
}

.item-container{
  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: space-between;
  min-width: 30vw;
}
</style>
  