<template>
  <div :style="tableStyle" class="overflow-y-auto">
    <table class="w-full">
      <thead>
      <tr>
        <slot name="header" />
      </tr>
      </thead>
      <tbody>
      <tr v-for="item in items"
        :key="item[keyName]"
        :class="rowClassName"
        @click="handleRowClick(item)">
        <slot name="items" :item="item" />
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    hover: Boolean,
    clickable: Boolean,
    items: {
      type: Array,
      default: () => []
    },
    keyName: {
      type: String,
      default: 'id'
    },
    onRowClick: Function,
    maxHeight: [String, Number]
  },
  computed: {
    tableStyle () {
      const { maxHeight } = this
      if (!maxHeight) return null
      return {
        maxHeight: `${maxHeight}px`
      }
    },
    rowClassName () {
      const { clickable, hover } = this
      return {
        'hover:bg-gray-100': hover,
        'cursor-pointer': clickable
      }
    }
  },
  methods: {
    handleRowClick (data) {
      this.$emit('onRowClick', data)
      // @TODO remove later
      const { onRowClick } = this
      if (onRowClick) onRowClick(data)
    }
  }
}
</script>

<style>
tr {
  border-bottom: 1px #eaeaea solid;
}
</style>
