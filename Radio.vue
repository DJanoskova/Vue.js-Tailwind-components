<template>
  <div>
    <label v-for="(option, index) in data"
      :class="[`inline-flex items-center`, {'mr-4': index < data.length - 1}]"
      :key="option.value">
      <input type="radio"
        class="form-radio text-primary-500"
        :name="name"
        :value="option.value"
        @change="handleChange"
        :checked="model === option.value">
      <span class="ml-2 text-gray-700">
        {{ option.label }}
      </span>
    </label>
  </div>
</template>

<script>
export default {
  props: {
    value: [String, Number, Object],
    data: Array,
    name: String
  },
  data () {
    return {
      model: this.value
    }
  },
  methods: {
    handleChange ({ target }) {
      this.model = target.value
    }
  },
  watch: {
    model () {
      this.$emit('input', this.model)
    }
  }
}
</script>
