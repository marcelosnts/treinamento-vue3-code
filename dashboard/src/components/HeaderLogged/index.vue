<template>
  <div class="flex items-center justify-between w-4/5 max-w-6xl py-10">
    <div class="w-28 lg:2-36">
      <img class="w-100" src="../../assets/images/logo_white.png" alt="feedbacker-logo">
    </div>
    <div class="flex">
      <ul class="flex list-none">
        <li
          @click="() => router.push({ name: 'Credentials' })"
          class="px-6 py-2 mr-2 font-bold text-white rounded-full cursor-pointer focus:outline-none"
        >
          Credentials
        </li>
        <li
          @click="() => router.push({ name: 'Feedbacks' })"
          class="px-6 py-2 mr-2 font-bold text-white rounded-full cursor-pointer focus:outline-none"
        >
          Feedbacks
        </li>
        <li
          @click="handleLogout"
          class="px-6 py-2 font-bold bg-white rounded-full cursor-pointer text-brand-main focus:outline-none"
        >
          {{logoutLabel}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue'
import { useRouter } from 'vue-router'
import useStore from '../../hooks/useStore'
import { cleanCurrentUser } from '../../store/user'

export default {
  setup () {
    const router = useRouter()
    const store = useStore('User')

    const logoutLabel = computed(() => {
      if (!store.currentUser.name) {
        return '...'
      } else {
        return `${store.currentUser.name} (logout)`
      }
    })

    function handleLogout () {
      window.localStorage.removeItem('token')
      cleanCurrentUser()
      router.push({ name: 'Home' })
    }

    return {
      router,
      logoutLabel,
      handleLogout
    }
  }
}
</script>
