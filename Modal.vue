<template>
  <transition name="modal">
    <div class="modal-backdrop fixed w-screen h-screen flex items-center justify-center"
      v-show="isOpen"
      :class="{open: isOpen}"
      @click="$emit('onClose')">
      <div class="modal-dialog" :class="{open: isOpen}" @click.stop>
        <Card :title="title" v-if="isOpen">
          <slot />
        </Card>
      </div>
    </div>
  </transition>
</template>

<script>
import Card from './Card'

export default {
  props: {
    isOpen: Boolean,
    title: String
  },
  components: { Card }
}
</script>
