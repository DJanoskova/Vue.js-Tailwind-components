<template>
  <Input v-model="model" :placeholder="placeholder" :label="label" :type="inputType" :disabled="disabled" />
</template>

<script>
import moment from 'moment'
import Input from './Input'

export default {
  props: {
    value: {
      type: [String, Object],
      default: ''
    },
    label: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'date'
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      model: ''
    }
  },
  created () {
    this.setValue()
  },
  methods: {
    setValue () {
      const { value } = this
      if (value) this.model = moment(value).format(this.inputFormat)
      else this.model = ''
    }
  },
  computed: {
    inputType () {
      switch (this.type) {
        case 'datetime':
          return 'datetime-local'
        default:
          return 'date'
      }
    },
    inputFormat () {
      switch (this.type) {
        case 'datetime':
          return 'YYYY-MM-DDTHH:mm'
        default:
          return 'YYYY-MM-DD'
      }
    }
  },
  watch: {
    model () {
      this.$emit('input', this.model)
    },
    value () {
      this.setValue()
    }
  },
  components: { Input }
}
</script>
