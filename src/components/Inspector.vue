<template>
  <div>
    <h1>Inspector</h1>
    <template v-if="node">
      <p>
        <span>
          <input type="checkbox" checked disabled>
        </span>
        <span>{{ node.Name }}</span>
      </p>
      <h3>Components</h3>
      <div v-if="node.Components.length > 0">
        <div v-for="(component, i) in node.Components" :key="i">
          <p>
            <span>
              <input type="checkbox" checked disabled>
            </span>
            <span>{{i + 1}} {{ component }}</span>
          </p>
        </div>
      </div>
      <div v-else>
        <p>no components</p>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    node: Object
  }
}
</script>

<style>

</style>