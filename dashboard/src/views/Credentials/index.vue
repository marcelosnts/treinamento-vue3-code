<template>
  <div class="flex justify-center w-full h-28 bg-brand-main">
    <header-logged />
  </div>

  <div class="flex flex-col items-center justify-center h-64 bg-brand-gray">
    <h1 class="text-4xl font-black text-center text-gray-800">Credentials</h1>
    <p class="text-lg text-center text-gray-800 font-regular">
      Instalation and credentials generation guide
    </p>
  </div>

  <div class="flex justify-center w-full h-full">
    <div class="flex flex-col w-4/5 max-w-6xl py-10">
      <h1 class="text-3xl font-black text-brand-darkgray">
        Installation and setup
      </h1>
      <p class="mt-10 text-lg text-gray-800 font-regular">
        This is your API key
      </p>

      <content-loader
        v-if="store.Global.isLoading || state.isLoading"
        class="rounded"
        width="600px"
        height="50px"
      />
      <div
        v-else
        class="flex py-3 pl-5 pr-20 mt-2 rounded justify-between items-center bg-brand-gray w-full lg:w-2/3"
      >
        <span>{{store.User.currentUser.apiKey}}</span>
        <div class="flex ml-20 mr-1">
          <icon
            name="copy"
            :color="brandColors.graydark"
            size="24"
            class="cursor-pointer"
          />
          <icon
            name="loading"
            :color="brandColors.graydark"
            size="24"
            class="cursor-pointer ml-3"
          />
        </div>
      </div>

      <p class="mt-5 text-lg text-gray-800 font-regular">
        Add this script at your site to start receiving feedbacks
      </p>

      <content-loader
        v-if="store.Global.isLoading || state.isLoading"
        class="rounded"
        width="600px"
        height="50px"
      />
      <div
        v-else
        class="py-3 pl-5 pr-20 mt-2 rounded bg-brand-gray justify-between items-center w-full lg:w-2/3 overflow-x-scroll"
      >
        <pre>&lt;script src="https://marcelosnts-feedbacker-widget.netlify.app?apy_key={{store.User.currentUser.apiKey}}"&gt;&lt;/script&gt;</pre>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'

import HeaderLogged from '../../components/HeaderLogged'
import ContentLoader from '../../components/ContentLoader'
import Icon from '../../components/Icon'
import useStore from '../../hooks/useStore'
import palette from '../../../palette'

export default {
  components: {
    HeaderLogged,
    ContentLoader,
    Icon
  },
  setup () {
    const store = useStore()
    const state = reactive({
      isLoading: false
    })

    return {
      state,
      store,
      brandColors: palette.brand
    }
  }
}
</script>
