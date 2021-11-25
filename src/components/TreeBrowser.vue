<template>
  <div>
    <div :style="style">
      <span v-if="hasChildrens" @click="nodeClicked">{{ expanded ? '&#9660;' : '&#9658;' }}</span>
      <span v-else>&#9671;</span>
      <span @click="nameClicked">{{ node.Name }} {{ node.Components.length }} {{ node.Childrens.length }}</span>
    </div>
    <template v-if="expanded">
      <TreeBrowser
        v-for="(child, i) in node.Childrens"
        :key="i"
        :node="child"
        :depth="depth + 1"
        :fullExpanded="expandChildrens"
        @objectClicked="(stack) => $emit('objectClicked', [node.Name, ...stack])"
      />
    </template>
  </div>
</template>

<script>
export default {
  name: "TreeBrowser",
  props: {
    node: Object,
    depth: {
      type: Number,
      default: 0
    },
    fullExpanded: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      expanded: false,
      expandChildrens: false
    }
  },
  created() {
    if (this.fullExpanded) {
      this.expanded = this.expandChildrens = true
    }
  },
  methods: {
    nodeClicked(event) {
      this.expanded = !this.expanded
      this.expandChildrens = event.altKey
    },
    nameClicked() {
      this.$emit("objectClicked", [this.node.Name])
    },
  },
  computed: {
    style() {
      return {
        "margin-left": this.depth * 20 + "px"
      }
    },
    hasChildrens() {
      return this.node.Childrens && this.node.Childrens.length > 0
    }
  }
}
</script>

<style scoped>
span {
  white-space: nowrap;
}
</style>