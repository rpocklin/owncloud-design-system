<template>
  <a class="oc-file" @click="onClick">
    <oc-icon :name="icon" variation="primary" class="uk-position-center-left" />
    <span class="oc-file-name" v-text="name" /><span v-if="extension" class="oc-file-extension"
      >.{{ extension }}</span
    >
  </a>
</template>
<script>
/**
 * Displays a file/folder together with the file type icon and the file extension.
 */
export default {
  name: "oc-file",
  status: "review",
  release: "1.0.0",
  props: {
    /**
     * The icon to be used.
     */
    icon: {
      type: String,
      required: false,
      default: "folder",
    },
    /**
     * The name of a file.
     * Please note that the name shall not hold the extension
     */
    name: {
      type: String,
      required: true,
      default: "",
    },
    /**
     * The extension of a file`.
     */
    extension: {
      type: String,
      required: false,
      default: "",
    },
  },
  methods: {
    onClick() {
      /**
       * This event is emitted when the user clicks a file
       * @type {string}
       */
      this.$emit("click", this.file)
    },
  },
}
</script>
<docs>
  ```vue
  <template>
    <section>
      <h3 class="uk-heading-divider">
        File examples
      </h3>
      <ul class="uk-list">
        <li>
          <oc-file icon="image" name="I love flowers" extension="jpg" />
        </li>
        <li>
          <oc-file icon="folder" name='Large folder' />
        </li>
        <li>
          <oc-file icon="image" name='Just kidding, I hate flowers.png' extension="png" />
        </li>
        <li>
          <oc-file icon="text" name='README' extension="md" />
        </li>
        <li>
          <oc-file icon="archive" name='package' extension="tar.gz" />
        </li>
        <li>
        </li>
      </ul>
      <h3 class="uk-heading-divider">
        Interactions
      </h3>
      <oc-file type="div" icon="text" :name="name" :extension="extension" @click="onChange"/>
    </section>
  </template>
  <script>
    export default {
      data: () => {
        return {
          name: 'Click me to change me',
          extension: '!!!',
          toggle: true
        }
      },
      methods: {
        onChange(val) {
          this.toggle = !this.toggle
          if (this.toggle) {
            this.name = 'New Image'
            this.extension = 'png'
          } else {
            this.name = 'New Textfile'
            this.extension = 'txt'
          }
        }
      }
    }
  </script>
  ```
</docs>