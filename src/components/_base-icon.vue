<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faSync, faUser } from '@fortawesome/free-solid-svg-icons'
import camelCase from 'lodash/camelCase'

export default {
  components: {
    FontAwesomeIcon,
  },
  props: {
    source: {
      type: String,
      default: 'font-awesome',
    },
    name: {
      type: String,
      required: true,
    },
  },
  computed: {
    // https://fontawesome.com/icons
    fontAwesomeIcon() {
      return {
        // Add new icons to this list as you need them
        sync: faSync,
        user: faUser,
      }[this.name]
    },
    // Gets a CSS module class, e.g. iconCustomLogo
    customIconClass() {
      return this.$style[camelCase('icon-custom-' + this.name)]
    },
  },
}
</script>

<template>
  <FontAwesomeIcon
    v-if="source === 'font-awesome'"
    :icon="fontAwesomeIcon"
    v-bind="$attrs"
  />
  <span
    v-else-if="source === 'custom'"
    :class="customIconClass"
  />
</template>
