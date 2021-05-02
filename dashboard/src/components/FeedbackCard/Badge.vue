<template>
  <span
    :class="classColor"
    class="p-2 font-black text-white uppercase rounded-full"
  >
    {{label}}
  </span>
</template>

<script>
import { computed } from 'vue'

export default {
  props: {
    type: { type: String, required: true }
  },
  setup (props) {
    const label = computed(() => {
      if (props.type === 'ISSUE') {
        return 'issue'
      }
      if (props.type === 'IDEA') {
        return 'idea'
      }

      return 'others'
    })

    const classColor = computed(() => {
      if (props.type === 'ISSUE') {
        return 'bg-brand-danger'
      }
      if (props.type === 'IDEA') {
        return 'bg-brand-warning'
      }

      return 'bg-brand-graydark'
    })

    return {
      label,
      classColor
    }
  }
}
</script>
