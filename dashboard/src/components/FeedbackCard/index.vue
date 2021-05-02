<template>
  <div
    @click="handleToggle"
    class="flex flex-col px-8 py-6 rounded cursor-pointer bg-brand-gray"
  >
    <div class="flex items-center justify-between w-full mb-8">
      <badge :type="feedback.type" />
      <span class="font-regular text-brand-graydark">
        {{getDiffTimeBetweenCurrentDate(feedback.createdAt)}}
      </span>
    </div>

    <div class="text-lg font-medium text-gray-800">
      {{feedback.text}}
    </div>

    <div
      v-if="state.isOpen"
      class="flex mt-8 animate__animated animate__fadeInUp animte__faster"
    >
      <div class="flex flex-col w-1/2">
        <div class="flex flex-col">
          <span class="font-bold text-gray-400 uppercase select-none">
            Page
          </span>
          <span class="font-medium text-gray-700 uppercase select-none">
            {{feedback.page}}
          </span>
        </div>
        <div class="flex flex-col">
          <span class="font-bold text-gray-400 uppercase select-none">
            Device
          </span>
          <span class="font-medium text-gray-700 uppercase select-none">
            {{feedback.device}}
          </span>
        </div>
      </div>
      <div class="flex flex-col w-1/2">
        <div class="flex flex-col">
          <span class="font-bold text-gray-400 uppercase select-none">
            Fingerprint
          </span>
          <span class="font-medium text-gray-700 uppercase select-none">
            {{feedback.fingerprint}}
          </span>
        </div>
      </div>
    </div>
    <div
      v-if="!state.isOpen"
      class="flex justify-end mt-8"
    >
      <icon name="chevron-down" size="24" :color="brandColors.graydark" />
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'

import Badge from './Badge'
import { getDiffTimeBetweenCurrentDate } from '../../utils/date'
import palette from '../../../palette'
import Icon from '../Icon'

export default {
  components: {
    Badge,
    Icon
  },
  props: {
    isOpened: { type: Boolean, default: false },
    feedback: { type: Object, required: true }
  },
  setup (props) {
    const state = reactive({
      isOpen: props.isOpened
    })

    function handleToggle () {

    }

    return {
      state,
      handleToggle,
      getDiffTimeBetweenCurrentDate,
      brandColors: palette.brand
    }
  }
}
</script>
