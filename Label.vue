<template>
  <label :class="classes">
    <slot />
  </label>
</template>

<script>
export default {
  props: {
    right: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    classes () {
      return [
        'block text-gray-500 font-bold mb-1 md:mb-0 pr-4',
        {
          'md:text-right': this.right
        }
      ]
    }
  }
}
</script>
