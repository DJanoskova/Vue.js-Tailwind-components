<template>
  <div>
    <Input v-model="tag" :placeholder="placeholder" :label="label" @keydown.enter.native="handleAdd" class="mb-1" />

    <div class="-mx-1">
      <Tag v-for="tag in model"
        :key="tag"
        class="m-1"
        size="small"
        @onClose="handleRemove(tag)"
        closable>
        {{ tag }}
      </Tag>
    </div>
  </div>
</template>

<script>
import Tag from './Tag'
import Input from './Input'

export default {
  props: {
    value: {
      type: Array,
      default: () => []
    },
    label: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: 'Press Enter to add'
    }
  },
  data () {
    return {
      model: this.value,
      tag: ''
    }
  },
  methods: {
    handleAdd (e) {
      const { tag } = this
      if (!tag) return

      e.preventDefault()

      const hasTag = this.model.find(t => t === tag)
      if (hasTag) return

      this.model.push(this.tag)
      this.tag = ''
    },
    handleRemove (tag) {
      this.model = this.model.filter(t => t !== tag)
    }
  },
  watch: {
    model () {
      this.$emit('input', this.model)
    }
  },
  components: { Input, Tag }
}
</script>
