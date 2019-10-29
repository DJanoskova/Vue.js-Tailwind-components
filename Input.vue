<template>
  <div>
    <FormLabel v-if="label">{{ label }}</FormLabel>
    <textarea v-if="type === 'textarea'" v-model="model" ref="input" :rows="rows" v-bind="inputAttr" />
    <input v-model="model" ref="input" v-bind="inputAttr" v-else />
  </div>
</template>

<script>
import FormLabel from './FormLabel'
export default {
  props: {
    type: {
      type: String,
      default: 'text'
    },
    value: [String, Number],
    label: String,
    placeholder: String,
    disabled: {
      type: Boolean,
      default: false
    },
    autofocus: Boolean,
    rows: [String, Number]
  },
  data () {
    return {
      model: this.value
    }
  },
  mounted () {
    if (this.autofocus) this.$refs.input.focus()
  },
  watch: {
    model () {
      this.$emit('input', this.model)
      this.$emit('change', this.model)
    },
    value () {
      this.model = this.value
    }
  },
  computed: {
    classes () {
      const { color, disabled } = this
      return [
        `bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 leading-tight focus:outline-none focus:bg-white`,
        {
          [`focus:border-${color}-500`]: !disabled,
          'text-gray-700': !disabled,
          'text-gray-500': disabled
        }
      ]
    },
    inputAttr () {
      const { type, placeholder, disabled } = this
      return {
        class: this.classes,
        type,
        placeholder,
        disabled
      }
    }
  },
  components: { FormLabel }
}
</script>
