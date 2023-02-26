<template>
  <!-- <p  ref="testref">helllo</p> -->
  <draggable
    class="node"
    tag="ul"
    :list="nodes"
    :group="{ name: 'g1' }"
    item-key="name"
  >
    <template #item="{ element }">
      <li>
        <div :id="element.name" class="item-container node_element">
          <div @click="nodeClicked(element)">
            <span class="pr-5">
              <i v-if="isExpanded(element)" class="bi bi-chevron-down">
                <i class="bi bi-folder2-open"></i>
              </i>

              <span v-else>
                <i v-if="element.children" class="bi bi-chevron-right">
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
          v-if="isExpanded(element) && element.children"
          :nodes="element.children"
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
    nodes: {
      required: true,
      type: Array,
    },
  },
  methods: {
    isExpanded(node) {
      return this.expanded.indexOf(node) !== -1;
    },
    nodeClicked(node) {
      let allElements = document.getElementsByClassName("node_element");
      for (var i = 0; i < allElements.length; i++) {
        allElements[i].style.backgroundColor = "transparent";
      }
      let catched_node = document.getElementById(node.name);
      catched_node.style.backgroundColor = "lightgray";
      catched_node.style.cursor = "pointer";

      // this.active = true;

      if (node.children) {
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
  padding-left: 0;
}

.type {
  margin-right: 10px;
}

.icon_button {
  background-color: transparent;
  border: none;
}

.item-container {
  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: space-between;
  min-width: 30vw;
}
</style>
