<template>
  <div>
    <input type="file" accept=".json" @change="onFileChange">
    <div class="container">
      <TreeBrowser
        v-if="hierarchy !== null"
        :node="hierarchy"
        @objectClicked="handleClick"
        style="overflow-y: scroll; height: 100vh; width: 50vw;"
      />
      <Inspector :node="selectedNode" />
    </div>
  </div>
</template>

<script>
import TreeBrowser from "./components/TreeBrowser.vue"
import Inspector from "./components/Inspector.vue"

export default {
  name: 'App',
  components: {
    TreeBrowser, Inspector
  },
  data() {
    return {
      hierarchy: null,
      selectedNode: null
    }
  },
  methods: {
    handleClick(stack) {
      // todo: find better way
      let result = this.hierarchy
      for (let i = 1; i < stack.length; i++) {
        result = result.Childrens.find(c => c.Name == stack[i])
      }
      this.selectedNode = result
    },
    onFileChange(event) {
      this.readFile(event.target.files[0]).then(text => this.hierarchy = JSON.parse(text))
    },
    readFile(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader()
        reader.onload = () => resolve(reader.result)
        reader.onerror = () => reject(reader.error)
        reader.readAsText(file)
      })
    },
  },
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
