<template>
  <component
    :is="type"
    :href="href"
    :to="to"
    :type="submit"
    :aria-label="ariaLabel"
    :class="$_ocButton_buttonClass"
    :disabled="disabled"
    @click="$_ocButton_onClick"
  >
    <!-- @slot Content of the button -->
    <slot />
  </component>
</template>

<script>
export default {
  name: "oc-button",
  status: "review",
  release: "1.0.0",
  props: {
    /**
     * The html element used for the button.
     * `button, a, router`
     */
    type: {
      type: String,
      default: "button",
      validator: value => {
        return value.match(/(button|a|router-link)/)
      },
    },
    /**
     * Disable the button
     */
    disabled: {
      type: Boolean,
      default: false,
    },
    /**
     * The size of the button. Defaults to medium.
     * `small, medium, large`
     */
    size: {
      type: String,
      default: null,
      validator: value => {
        return value.match(/(small|large)/)
      },
    },
    /**
     * When setting the button’s type to a link, use this option to give a href.
     */
    href: {
      type: String,
      default: null,
    },
    /**
     * When setting the button’s type to a router-link, use this option to give a to.
     */
    to: {
      type: Object,
      default: null,
    },
    /**
     * The aria-label of the button.
     */
    ariaLabel: {
      type: String,
      default: null,
    },
    /**
     * Set the button’s type to “submit”.
     */
    submit: {
      type: String,
      default: null,
      validator: value => {
        return value.match(/(null|submit)/)
      },
    },
    /**
     * Style variation to give additional meaning.
     * `primary, danger`
     */
    variation: {
      type: String,
      default: "default",
      validator: value => {
        return value.match(/(default|primary|danger|raw)/)
      },
    },
    /**
     * Don't add the element class to this element.
     */
    stopClassPropagation: {
      type: Boolean,
      default: false,
    },
    /**
     * How to justify content within the button. Defaults to center.
     * `left, center, right, space-around, space-between, space-evenly`
     */
    justifyContent: {
      type: String,
      default: "center",
      validator: value => {
        return value.match(/(left|center|right|space-around|space-between|space-evenly)/)
      }
    },
    /**
     * Distance between children of the button. Defaults to small. Might be overruled by justify-content value.
     * `xsmall, small, normal, medium, large, xlarge`
     */
    gapSize: {
      type: String,
      default: "small",
      validator: value => {
        return value.match(/(xsmall|small|normal|medium|large|xlarge)/)
      }
    }
  },
  computed: {
    $_ocButton_buttonClass() {
      if (this.stopClassPropagation) return ""

      let classes = ["oc-button", `oc-button-justify-content-${this.justifyContent}`, `oc-button-gap-${this.gapSize}`]

      if (this.variation && !this.disabled) classes.push(`oc-button-${this.variation}`)

      if (this.disabled) classes.push("oc-button-default")

      if (this.size && this.variation !== "raw") classes.push(`oc-button-${this.size}`)

      return classes
    },
  },
  methods: {
    $_ocButton_onClick(event) {
      this.$emit("click", event)
    }
  }
}
</script>
<docs>
Buttons are generally used for interface actions. Suitable for all-purpose use.

Defaults to appearance that has white background with blue border.
Primary style should be used only once per view for main call-to-action.
All buttons are built with a css grid which ensures that there will be a pre-defined gutter between all child items.

## Accessibility
### Distinction when to use a `<button>`, when to use an `<a>`

Regardless of the visual representation the following differentiation should be made if in doubt what to choose.

- an anchor/link changes the location, be it internally on the website, or to another resource/document/route.
- a button does change the state of the website, e.g.: adds, deletes, opens, ...

### Accessible name
The accessible name ([explainer for the term](https://developer.paciellogroup.com/blog/2017/04/what-is-an-accessible-name/)) of a button is derived from several sources. Right now, only two of them are relevant:

1. The value of the `aria-label` attribute
2. The text between the opening and closing tag, `<button>This text here</button>`

When an aria-label attribute exists, its value will override the button text. So in this case, the accessible name would be "foo": `<button aria-label="foo">Bar</button>`, although visual users will see "Bar". This difference between accessible name and visual name is a problem for a certain type of assistive technology ([explainer for the term](https://en.wikipedia.org/wiki/Assistive_technology)), this is why the [WCAG success criterion 2.5.3, "Label in name"](https://www.w3.org/TR/WCAG21/#label-in-name) exists. This difference should be avoided, if it can't, W3C recommends that the accessible name should start with visible label.

### Icon-only button

Every button has to have an accessible name. It cannot be provided by a text between the button tags (for example, because it is an icon button; see "Upload" example below), the accessible name has to be provided by `aria-label`.

```js
  <h3 class="uk-heading-divider">
    Button Types
  </h3>
  <div class="uk-flex">
    <oc-button  class="uk-margin-small-right" v-text="'Default button'" />
    <oc-button variation="primary" class="uk-margin-small-right">Primary button</oc-button>
    <oc-button variation="danger" class="uk-margin-small-right">
      <oc-icon name="delete" aria-hidden="true" />
      Danger Button
    </oc-button>
    <oc-button disabled class="uk-margin-small-right">Disabled button</oc-button>
    <oc-button variation="raw">Raw button</oc-button>
  </div>

  <h3 class="uk-heading-divider">
    Button sizes
  </h3>
  <div class="uk-flex">
    <oc-button size="large" class="uk-margin-small-right">Large</oc-button>
    <oc-button size="small" class="oc-align-self-center">Small</oc-button>
  </div>

  <h3 class="uk-heading-divider">
    Button with icons
  </h3>
  <div class="uk-flex">
    <oc-button class="uk-margin-small-right">
      <oc-icon name="home" aria-hidden="true" />
      Home
    </oc-button>
    <oc-button variation="primary" class="uk-margin-small-right">
      Select
      <oc-icon name="expand_more" aria-hidden="true" />
    </oc-button>
    <oc-button variation="primary" aria-label="Upload a file">
      <oc-icon name="cloud_upload" />
    </oc-button>
  </div>

  <h3 class="uk-heading-divider">
    Using buttons in a group
  </h3>
  <div class="oc-button-group">
    <oc-button variation="primary">Hello</oc-button>
    <oc-button>
      <oc-icon name="folder" />
      Demo Button
    </oc-button>
    <oc-button variation="danger">Delete</oc-button>
  </div>
```
</docs>
