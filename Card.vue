<template>
  <div class="rounded overflow-hidden shadow-md bg-white">
    <img class="w-full" :src="image.src" :alt="image.alt" v-if="image">

    <div class="px-6 py-4">
      <div class="mb-2 text-gray-700 flex justify-between items-center" v-if="title">
        <span class="font-bold text-xl">
          {{ title }}
        </span>

        <slot name="actionButton" />
      </div>
      <div class="text-gray-600 text-base">
        <slot />
      </div>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    image: {
      type: Object,
      default: null
    },
    title: {
      type: String,
      default: ''
    }
  },
  computed: {
    hasButtons () {
      return this.$slots.buttons
    }
  }
}
</script>
