<script>
import { defineComponent, computed } from 'vue'
import props from '../utils/props'

export default defineComponent({
  props: {
    ...props,
    class: String,
    cols: String, // '2cols'
    hideTitleRow: Boolean,
  },
  setup(props) {
    const gridColsSize = computed(() => {
      if (!props.cols) return null
      switch (props.cols) {
        case '1-1':
          return 'grid-cols-2'
        case '1-2':
          return 'grid-cols-[1fr_2fr]'
        case '2-1':
          return 'grid-cols-[2fr_1fr]'
        default:
          return props.cols
      }
    })

    return {
      gridColsSize,
    }
  },
})
</script>

<template>
  <div
    class="slidev-layout grid gap-y-3 gap-x-5 default"
    :class="[!hideTitleRow ? 'grid-rows-[60px_1fr]' : null, gridColsSize]"
  >
    <div v-if="!hideTitleRow" :class="cols ? 'col-span-2' : null">
      <h1>{{ $frontmatter.title }}</h1>
    </div>
    <div>
      <slot />
    </div>
    <div v-if="cols">
      <slot name="right" />
    </div>
  </div>
</template>

<style lang="postcss"></style>
