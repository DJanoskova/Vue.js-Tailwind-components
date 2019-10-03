<template>
  <div>
    <FormLabel v-if="label">
      {{ label }}
    </FormLabel>

    <div class="relative">
      <select
        :class="classes"
        v-model="model"
        @change="$emit('change', $event)">
        <option v-if="placeholder" disabled value="">{{ placeholder }}</option>
        <slot />
      </select>
      <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
        <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
          <path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
import FormLabel from './FormLabel'

export default {
  props: {
    value: [String, Number],
    label: String,
    placeholder: {
      type: String,
      default: ''
    },
    size: {
      type: String,
      default: 'normal'
    }
  },
  data () {
    return {
      model: this.value
    }
  },
  watch: {
    model () {
      this.$emit('input', this.model)
    },
    value () {
      this.model = this.value
    }
  },
  computed: {
    classes () {
      const { size } = this
      const classes = ['block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500']
      switch (size) {
        case 'small':
          classes.push('py-2 px-3 pr-6')
          break
        default:
          classes.push('py-3 px-4 pr-8')
          break
      }
      return classes
    }
  },
  components: {
    FormLabel
  }
}
</script>
