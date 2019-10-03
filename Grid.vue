<template>
  <div :class="classes">
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    spacing: [Number, String]
  },
  computed: {
    classes () {
      const { spacing } = this
      return ['flex flex-wrap', `-mx-${spacing}`]
    }
  }
}
</script>
