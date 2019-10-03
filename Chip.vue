<template>
  <span :class="classes">
    <span :class="circleClasses">
      <slot name="icon" />
    </span>
    <span class="pr-3 pl-2">
      <slot />
    </span>
    <Button v-if="closable" icon="close-outline" size="xsmall" class="mr-1" @click="$emit('onClose')" />
  </span>
</template>

<script>
import Button from './Button'

export default {
  props: {
    color: {
      type: String,
      default: 'gray'
    },
    closable: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    classes () {
      const { color } = this
      return [
        `bg-${color}-200 h-8 inline-flex text-sm items-center rounded-full overflow-hidden leading-none`
      ]
    },
    circleClasses () {
      const { color } = this
      return [
        `bg-${color}-300 w-8 h-full rounded-full`
      ]
    }
  },
  components: { Button }
}
</script>
