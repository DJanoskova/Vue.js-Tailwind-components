<template>
  <div :class="classes">
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    xs: {
      type: [Number, String],
      default: 'full'
    },
    sm: {
      type: [Number, String],
      default: ''
    },
    md: {
      type: [Number, String],
      default: ''
    },
    lg: {
      type: [Number, String],
      default: ''
    },
    xl: {
      type: [Number, String],
      default: ''
    }
  },
  computed: {
    classes () {
      const { spacing, mb } = this.$parent
      const { xs, sm, md, lg, xl } = this
      const classes = [
        `w-${xs}`
      ]
      if (sm) classes.push(`sm:w-${sm}`)
      if (md) classes.push(`md:w-${md}`)
      if (lg) classes.push(`lg:w-${lg}`)
      if (xl) classes.push(`lg:w-${xl}`)
      if (spacing) classes.push(`px-${spacing}`)
      if (mb) classes.push(`mb-${mb}`)
      return classes
    }
  }
}
</script>
