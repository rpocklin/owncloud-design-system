<template>
  <li :class="$_ocSidebarNavItem_class">
    <router-link
      :to="target"
    >
      <oc-icon :name="icon" aria-hidden="true" />
      <slot name="default" />
    </router-link>
    <ul class="uk-nav-sub" v-if="$slots.subnav">
      <slot name="subnav" />
    </ul>
  </li>
</template>
<script>
import OcIcon from "./OcIcon.vue"

export default {
  name: "oc-sidebar-nav-item",
  status: "prototype",
  release: "1.0.0",
  components: {
    OcIcon
  },
  props: {
    active: {
      type: Boolean,
      required: false,
      default: false,
    },
    target: {
      type: String,
      required: false,
      default: null,
    },
    icon: {
      type: String,
      required: true,
      default: "",
    },
    isolate: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  computed: {
    $_ocSidebarNavItem_class() {
      let classes = []
      if (this.$slots.subnav) {
        classes.push("uk-parent")
      }
      if (this.active) {
        classes.push("uk-active")
      }
      if (this.isolate) {
        classes.push("uk-margin-medium-top")
      }
      return classes
    },
  },
}
</script>
<docs>
  ```jsx
  <oc-sidebar-nav-item target="home" icon="close" active>Demo Item</oc-sidebar-nav-item>
  <oc-sidebar-nav-item target="home" icon="edit">Demo Item</oc-sidebar-nav-item>
  ```
</docs>
