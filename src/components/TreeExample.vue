<template>
  <!-- data tree -->
  <div>
    <h1>Data Tree</h1>
    <button @click="printObj">console.log</button>
    <br />
    <Tree
      id="my-tree-id"
      ref="my-tree"
      :custom-options="myCustomOptions"
      :custom-styles="myCustomStyles"
      :nodes="treeDisplayData"
    ></Tree>
  </div>


  <!-- data table    -->
  <div></div>
</template>
  
  <script>
import Tree from "vuejs-tree";

export default {
  name: "TreeExample",
  components: {
    Tree,
  },
  data: function () {
    return {
      ourData: [
        {
          "Admin": {
            "people": {
              "providers": "",
              "Users": {
                "manageusers": {
                  "General": "",
                  "Identity": "",
                  "clinic": "",
                  "securityRoles": "",
                },
              },
            },
          },
        },
         {
          "Calender": {
            "": "",
         } 
        },
          {
            "Requests": {
            "": "",
          },
          }
         
        
      ],
      activetab: "1",
       //root1 : Object.keys( this.ourData[1]).toString() ,
       x:'calendar',
      treeDisplayData: [
        {
          text: "\""+ "this.ourData[1].toString" +"\"",
          state: { checked: false, selected: false, expanded: false },
          id: 1,
          checkable: false,
          nodes: [
            {
              text: "Child 1",
              state: { checked: true, selected: false, expanded: false },
              id: 3,
              nodes: [
                {
                  text: "Grandchild 1",
                  state: { checked: false, selected: false, expanded: false },
                  id: 5,
                },
                {
                  text: "Grandchild 2",
                  state: { checked: false, selected: false, expanded: false },
                  id: 6,
                },
              ],
            },
            {
              text: "Child 2",
              state: { checked: false, selected: false, expanded: false },
              id: 4,
            },
          ],
        },
        {
          text: "Root 2",
          state: { checked: false, selected: false, expanded: false },
          id: 2,
        },
        {
          text: "Root 3",
          state: { checked: false, selected: false, expanded: false },
          id: 2,
        },
      ],
    };
  },
  computed: {
    myCustomStyles() {
      return {
        tree: {
          style: {
            height: "auto",
            maxHeight: "300px",
            overflowY: "visible",
            display: "inline-block",
            textAlign: "left",
          },
        },
        row: {
          style: {
            width: "500px",
            cursor: "pointer",
          },
          child: {
            class: "",
            style: {
              height: "35px",
            },
            active: {
              style: {
                height: "35px",
              },
            },
          },
        },
        rowIndent: {
          paddingLeft: "20px",
        },
        text: {
          // class: "" // uncomment this line to overwrite the 'capitalize' class, or add a custom class
          style: {},
          active: {
            style: {
              "font-weight": "bold",
              color: "#2ECC71",
            },
          },
        },
      };
    },
    myCustomOptions() {
      return {
        treeEvents: {
          expanded: {
            state: false,
          },
          collapsed: {
            state: false,
          },
          selected: {
            state: true,
            fn: this.mySelectedFunction,
          },
          checked: {
            state: true,
            fn: this.myCheckedFunction,
          },
        },
        events: {
          expanded: {
            state: true,
          },
          selected: {
            state: true,
          },
          checked: {
            state: true,
          },
          editableName: {
            state: true,
            calledEvent: "expanded",
          },
        },
        addNode: {
          state: true,
          fn: this.addNodeFunction,
          appearOnHover: false,
        },
        editNode: { state: false, fn: null, appearOnHover: false },
        deleteNode: {
          state: true,
          fn: this.deleteNodeFunction,
          appearOnHover: true,
        },
        showTags: true,
      };
    },
  },
  mounted() {
    this.$refs["my-tree"].expandNode(1);
    
  },
  methods: {
     printObj( ) {
      console.log( Object.keys( this.ourData[1]).toString())


    },
    myCheckedFunction: function (nodeId, state) {
      console.log(`is ${nodeId} checked ? ${state}`);
      console.log(this.$refs["my-tree"].getCheckedNodes("id"));
      console.log(this.$refs["my-tree"].getCheckedNodes("text"));
    },
    mySelectedFunction: function (nodeId, state) {
      console.log(`is ${nodeId} selected ? ${state}`);
      console.log(this.$refs["my-tree"].getSelectedNode());
    },
    deleteNodeFunction: function (node) {
      const nodePath = this.$refs["my-tree"].findNodePath(node.id);
      const parentNodeId = nodePath.slice(-2, -1)[0];
      if (parentNodeId === undefined) {
        // 'root' node
        const nodeIndex =
          this.$refs["my-tree"].nodes.findIndex((x) => x.id !== node.id) - 1;
        this.$refs["my-tree"].nodes.splice(nodeIndex, 1);
      } else {
        // child node
        const parentNode = this.$refs["my-tree"].findNode(parentNodeId);
        const nodeIndex =
          parentNode.nodes.findIndex((x) => x.id !== node.id) - 1;
        parentNode.nodes.splice(nodeIndex, 1);
      }
      console.log("example: remove node", node.id);
    },
    addNodeFunction: function (node) {
      const newNode = {
        text: "Grandchild 2",
        id: Math.floor(Math.random() * 100),
        state: { checked: false, selected: false, expanded: false },
      };
      console.log("example: add node", newNode);
      if (node.nodes === undefined) {
        node.nodes = [newNode];
      } else {
        node.nodes.push(newNode);
      }
    },
  },
};
</script>

  <style>
/* Import Google Font */
@import url(https://fonts.googleapis.com/css?family=Nunito+Sans);

/* RESET */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 620px;
  min-width: 420px;
  margin: 40px auto;
  font-family: "Nunito Sans", Arial, Helvetica, sans-serif;
  font-size: 0.9em;
  color: #888;
}

/* Style the tabs */
.tabs {
  overflow: hidden;
  margin-bottom: -2px; /* hide bottom border */
  margin-left: 24px;
}

.tabs a {
  float: left;
  cursor: pointer;
  padding: 12px 24px;
  transition: background-color 0.2s;
  border: 1px solid #ccc;
  border-right: none;
  background-color: #f1f1f1;
  border-radius: 10px 10px 0 0;
  font-weight: bold;
}
.tabs a:last-child {
  border-right: 1px solid #ccc;
}

/* Change background color of tabs on hover */
.tabs a:hover {
  background-color: #aaa;
  color: #fff;
}

/* Styling for active tab */
.tabs a.active {
  background-color: #fff;
  color: #484848;
  border-bottom: 2px solid #fff;
  cursor: default;
}

/* Style the tab content */
.tabcontent {
  padding: 30px 50px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 4px 4px 8px #e1e1e1;
}

.tabcontent td {
  padding: 0.3em 0.4em;
  color: #484848;
}
.tabcontent td.legend {
  color: #888;
  font-weight: bold;
  text-align: right;
}
.tabcontent .map {
  height: 173px;
  width: 220px;
  background: #d3eafb;
  margin-left: 60px;
  border: 1px solid #ccc;
  border-radius: 10px;
}
.data {
  width: 120px;
}
</style>