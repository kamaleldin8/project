<template>
  <div id="app">
  
   
  </div>
 
 


    <div><TreeExample /></div>

    <div id="tabs"><TabberComponent/></div>

    <h1>Vue Tree Browser</h1>
      <div  style="margin-left: 25%;margin-bottom: 25%;" id="app">
    <DataTreeMarwa 
      :nodes="root"
      @onClick="nodeWasClicked"
    />
  </div>




  
</template>

<script>
import TreeExample from "./components/TreeExample";
import TabberComponent from "./components/TabberComponent"
import DataTreeMarwa from "./components/DataTreeMarwa.vue";
import rootData from "./root.json";


export default {
  data(){
    return{
        root:rootData
    }
  },
 
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
      //alert(node.name);
    },
  },
  
  name: "App",
  components: {
    TreeExample,
    TabberComponent,
    DataTreeMarwa
   
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


















<!-- <template>
  <div>
    <DxTreeView
      id="treeview"
      :items="products"
      :width="500"
      :search-enabled="true"
      :search-mode="searchMode"
    />
    <div class="options">
      <div class="caption">Options</div>
      <div class="option">
        <span>Search mode</span>
        <DxSelectBox
          :items="options"
          v-model:value="searchMode"
        />
      </div>
    </div>
  </div>
</template>
<script>

import DxTreeView from 'devextreme-vue/tree-view';
import DxSelectBox from 'devextreme-vue/select-box';

import { products } from './data.js';

export default {
  components: {
    DxSelectBox,
    DxTreeView,
  },
  data() {
    return {
      products,
      options: ['contains', 'startswith', 'equals'],
      searchMode: 'contains',
    };
  },
};
</script>
<style scoped>
#treeview {
  height: 400px;
}

.options {
  padding: 20px;
  position: absolute;
  bottom: 0;
  right: 0;
  width: 260px;
  top: 0;
  background-color: #f5f5f5;
}

.caption {
  font-size: 18px;
  font-weight: 500;
}

.option {
  margin-top: 10px;
}

.option > .dx-selectbox {
  display: inline-block;
  vertical-align: middle;
  max-width: 350px;
  width: 100%;
  margin-top: 5px;
}
</style> -->
