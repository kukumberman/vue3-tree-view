<template>
  <div class="container">
    <TreeBrowser
      :node="hierarchy"
      @objectClicked="handleClick"
      style="overflow-y: scroll; height: 100vh; width: 50vw;"
    />
    <Inspector :node="selectedNode" />
  </div>
</template>

<script>
import TreeBrowser from "./components/TreeBrowser.vue"
import Inspector from "./components/Inspector.vue"

import data from "./json/OfflinePlayer(Clone).json"
//import data from "./data.json"

export default {
  name: 'App',
  components: {
    TreeBrowser, Inspector
  },
  data() {
    return {
      hierarchy: data,
      selectedNode: null
    }
  },
  methods: {
    handleClick(stack) {
      // todo: find better way
      let result = data
      for (let i = 1; i < stack.length; i++) {
        result = result.Childrens.find(c => c.Name == stack[i])
      }
      this.selectedNode = result
    }
  },
  computed: {
    clickedElement() {
      return this.stack.join(" > ")
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

.container {
  display: flex;
  
}
</style>
