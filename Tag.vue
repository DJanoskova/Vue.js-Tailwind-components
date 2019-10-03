<template>
  <span :class="classes">
    <slot />
    <span v-if="closable" @click="$emit('onClose')" :class="closeClasses" :style="closeStyle">
      x
    </span>
  </span>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: 'gray'
    },
    closable: {
      type: Boolean,
      default: false
    },
    size: {
      type: String,
      default: 'base'
    },
    clickable: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    classes () {
      const { color, size, clickable } = this
      return [
        {
          'text-sm': size === 'base',
          'text-xs': size === 'small'
        },
        `bg-${color}-100`,
        `border border-${color}-300`,
        `text-${color}-500`,
        'py-1 px-2 rounded uppercase font-medium whitespace-no-wrap inline-flex',
        {
          [`hover:bg-${color}-200`]: clickable,
          [`border border-${color}-400`]: clickable,
          'cursor-pointer': clickable
        }
      ]
    },
    closeClasses () {
      const { color } = this
      return [
        `text-${color}-400`,
        `hover:text-${color}-500`,
        'cursor-pointer lowercase py-1 px-2 -my-1 -mr-2'
      ]
    },
    closeStyle () {
      return {
        position: 'relative',
        top: '-0.1em',
        transform: 'scale(1.1)'
      }
    }
  }
}
</script>
