<template>
  <span
    class="copy-button-container"
    @click="on_copy"
  >
    <span
      class="copy-button-content"
      v-if="!buttonBefore"
    >
      <b-tooltip
        :label="tooltip_label"
        type="is-light"
        position="is-bottom"
      >
        <slot />
      </b-tooltip>
    </span>

    <b-tooltip
      :label="tooltip_label"
      type="is-light"
      position="is-bottom"
      class="is-button-tooltip"
      aria-hidden="true"
    >
      <svg
        viewBox="0 0 20 20"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        class="copy-button"
      >
        <g
          id="Page-1"
          stroke="none"
          stroke-width="1"
          fill="none"
          fill-rule="evenodd"
        >
          <g id="icon-shape">
            <path d="M12.9728369,2.59456737 C12.7749064,1.12946324 11.5193533,0 10,0 C8.48064666,0 7.2250936,1.12946324 7.02716314,2.59456737 L5,3 L5,4 L3.99406028,4 C2.89451376,4 2,4.8927712 2,5.99406028 L2,18.0059397 C2,19.1054862 2.8927712,20 3.99406028,20 L16.0059397,20 C17.1054862,20 18,19.1072288 18,18.0059397 L18,5.99406028 C18,4.89451376 17.1072288,4 16.0059397,4 L15,4 L15,3 L12.9728369,2.59456737 Z M5,6 L4,6 L4,18 L16,18 L16,6 L15,6 L15,7 L5,7 L5,6 Z M10,4 C10.5522847,4 11,3.55228475 11,3 C11,2.44771525 10.5522847,2 10,2 C9.44771525,2 9,2.44771525 9,3 C9,3.55228475 9.44771525,4 10,4 Z" />
          </g>
        </g>
      </svg>
    </b-tooltip>

    <span
      class="copy-button-content"
      v-if="buttonBefore"
    >
      <b-tooltip
        :label="tooltip_label"
        type="is-light"
        position="is-bottom"
      >
        <slot />
      </b-tooltip>
    </span>
  </span>
</template>

<script>
export default {
  props: {
    copy: {
      type: String,
      required: true
    },
    label: {
      type: String,
      default: 'Copier'
    },
    buttonBefore: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      tooltip_label: null
    }
  },
  mounted () {
    this.tooltip_label = this.label
  },
  methods: {
    on_copy () {
      navigator.clipboard.writeText(this.copy)
      this.tooltip_label = 'Copié !'
      setTimeout(() => { this.tooltip_label = this.label }, 2000)
    }
  }
}
</script>

<style lang="sass">
@import '~bulma/sass/utilities/_all'
@import "zestedesavoir-standards"

.copy-button-container
  display: inline-flex
  align-items: center
  cursor: pointer

  .b-tooltip.is-button-tooltip
    position: relative

    .copy-button
      height: 1em

      path
        fill: $grey-400

  &:hover svg.copy-button g path
    fill: $grey-600 !important
</style>
