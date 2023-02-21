<template>
  <!-- <draggable class="dragArea" tag="div" :list="nodes"> -->
  <div
    v-for="node in nodes"
    :key="node.name"
    :style="{ 'margin-left': `${depth * 20}px` }"
    class="node"
  >
    <span class="type" @click="nodeClicked(node)">
      <!-- Expanded -->

      <i v-if="isExpanded(node)" class="bi bi-chevron-down">
        <i class="bi bi-folder2-open"></i>
      </i>

      <!-- not expanded -->
      <i v-else class="bi bi-chevron-right">
        <i v-if="node.children" class="bi bi-folder"></i>
        <i v-else class="bi bi-file-text"></i>
      </i>

      <!-- <img src="@/assets/foldericon.svg" width="200px" height="200px"/> -->
    </span>
    <!-- <span class="type">&#9671;</span> -->
    <span class="test">{{ node.name }}</span>
    <TreeBrowser
      v-if="isExpanded(node) && node.children"
      :nodes="node.children"
      :depth="depth + 1"
      @onClick="(node) => $emit('onClick', node)"
    />
  </div>
  <!-- </draggable> -->
</template>

<script>
//  import draggable from "vuedraggable";

// import * as ColorHash from "color-hash";
// const colorHash = new ColorHash();

export default {
  name: "TreeBrowser",
  props: {
    nodes: Array,
    depth: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      expanded: [],
    };
  },
  methods: {
    isExpanded(node) {
      return this.expanded.indexOf(node) !== -1;
    },
    nodeClicked(node) {
      if (node.children) {
        if (!this.isExpanded(node)) {
          this.expanded.push(node);
        } else {
          this.expanded.splice(this.expanded.indexOf(node));
        }
      }
    },
    // getStyle(node) {
    //   let color = "red";
    //   if (!node.children) {
    //     color = colorHash.hex(node.name.split(".")[1]);
    //   }
    //   return {
    //     color,
    //   };
    // },
  },
  components: {
    // draggable,
  },
  computed: {},
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
.test {
}
</style>
