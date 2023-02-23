<template>
    <p  ref="testref">helllo</p>
  <draggable
    class="node"
    tag="ul"
    :list="tasks"
    :group="{ name: 'g1' }"
    item-key="name"
  >
    <template #item="{ element }">
      <li>
        <div @click="nodeClicked(element)">
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
          <span class="p-1"  ref="selectedSpan">{{ element.name }}</span>
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
    //   const selectedItem = this.$refs.selectedSpan.filter(
    //     (item) => item.innerText === node.name
    //   );

      console.log( this.$refs);
      this.active = true;

      if (node.tasks) {
        if (!this.isExpanded(node)) {
        //   selectedItem[0].style.color = "green";
          this.expanded.push(node);
        } else {
          this.expanded.splice(this.expanded.indexOf(node));
        //   selectedItem[0].style.color = "";
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
</style>
  