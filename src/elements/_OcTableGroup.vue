<template>
  <tbody>
    <slot />
  </tbody>
</template>
<script>
export default {
  name: "oc-table-group",
  status: "review",
  release: "1.0.0",
  props: {
    group: {
      type: String,
      required: false,
      default: "tbody",
    },
  },
}
</script>
<style scoped>
div {
  display: table-row-group;
}

.oc-table-header-group {
  display: table-header-group;
}
.oc-table-header-group {
  display: table-header-group;
}
</style>
