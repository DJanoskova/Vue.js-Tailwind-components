<template>
  <button :type="type" :class="classNames" @click.stop="$emit('click')" :disabled="disabled">
    <i :class="`eva eva-${icon}`" v-if="icon" />
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: 'gray'
    },
    size: {
      type: String,
      default: 'normal'
    },
    classes: {
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    },
    type: {
      type: String,
      default: 'button'
    },
    variant: {
      type: String,
      default: 'contained'
    },
    shadow: Boolean,
    icon: String,
    tooltip: String
  },
  computed: {
    classNames () {
      const { disabled, color, classes, variant, icon, shadow, size } = this
      const classNames = [
        {
          'cursor-not-allowed opacity-50': disabled,
          'focus:shadow-outline': !disabled
        },
        {
          'rounded': !icon,
          'rounded-full inline-flex items-center': icon
        },
        `focus:outline-none leading-none`,
        classes
      ]

      switch (size) {
        case 'xsmall':
          classNames.push(
            `py-1`,
            {
              'px-3': !icon,
              'px-1': icon
            }
          )
          break
        case 'small':
          classNames.push(
            `py-2`,
            {
              'px-4': !icon,
              'px-2': icon
            }
          )
          break
        case 'normal':
        default:
          classNames.push(
            `py-2`,
            {
              'px-4': !icon,
              'text-lg px-2': icon
            }
          )
      }

      switch (variant) {
        case 'contained':
          classNames.push(
            {
              shadow: !disabled,
              [`hover:bg-${color}-400`]: !disabled
            },
            `bg-${color}-500`,
            'text-white',
            'font-bold')
          break
        case 'simple':
          classNames.push(
            `text-${color}-500`,
            'bg-transparent',
            `hover:bg-${color}-100`,
            `hover:border-${color}-500`
          )
          break
        case 'light':
          classNames.push(
            `text-${color}-500`,
            `bg-${color}-100`,
            `hover:bg-${color}-200`,
            `hover:border-blue-500`,
            `border border-${color}-300`
          )
          break
        default:
          break
      }

      if (shadow) classNames.push('shadow')

      return classNames
    }
  }
}
</script>
