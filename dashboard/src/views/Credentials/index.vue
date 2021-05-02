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
        <span v-if="state.hasError">Error on api key load</span>
        <span v-else>{{store.User.currentUser.apiKey}}</span>
        <div class="flex ml-20 mr-1" v-if="!state.hasError">
          <icon
            name="copy"
            @click="handleCopy"
            :color="brandColors.graydark"
            size="24"
            class="cursor-pointer"
          />
          <icon
            name="loading"
            @click="handleGenerateApiKey"
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
        <span v-if="state.hasError">Error on script load</span>
        <pre v-else>&lt;script src="https://marcelosnts-feedbacker-widget.netlify.app?apy_key={{store.User.currentUser.apiKey}}"&gt;&lt;/script&gt;</pre>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, watch } from 'vue'
import { useToast } from 'vue-toastification'

import HeaderLogged from '../../components/HeaderLogged'
import ContentLoader from '../../components/ContentLoader'
import Icon from '../../components/Icon'
import useStore from '../../hooks/useStore'
import palette from '../../../palette'
import services from '../../services'
import { setApiKey } from '../../store/user'

export default {
  components: {
    HeaderLogged,
    ContentLoader,
    Icon
  },
  setup () {
    const store = useStore()
    const toast = useToast()
    const state = reactive({
      hasError: false,
      isLoading: false
    })

    watch(() => store.User.currentUser, () => {
      if (!store.Global.isLoading && !store.User.currentUser.apiKey) {
        handleError(true)
      }
    })

    function handleError (error) {
      state.hasError = !!error
      state.isLoading = false
    }

    async function handleGenerateApiKey () {
      try {
        state.isLoading = true

        const { data } = await services.users.generateApiKey()

        setApiKey(data.apiKey)

        state.isLoading = false
      } catch (error) {
        handleError(error)
      }
    }

    async function handleCopy () {
      toast.clear()

      try {
        await navigator.clipboard.writeText(store.User.currentUser.apiKey)
        toast.success('Copied to clipboard!')
      } catch (error) {
        handleError(error)
      }
    }

    return {
      state,
      store,
      handleGenerateApiKey,
      handleCopy,
      brandColors: palette.brand
    }
  }
}
</script>
