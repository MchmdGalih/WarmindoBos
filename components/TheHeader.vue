<template>
  <nav
    class="flex flex-wrap sm:flex-nowrap justify-start sm:justify-between px-10 items-center w-full h-20 text-white bg-red-600 fixed z-10 top-0 left-0"
  >
    <div class="w-[90%] text-center sm:w-max sm:text-start">
      <h1 class="text-4xl sm font-logo font-bold">
        <nuxt-link to="/"
          >Warmi<span class="text-yellow-400">ndo</span></nuxt-link
        >
      </h1>
    </div>
    <ul
      class="hidden sm:flex flex-1 mr-4 gap-3 cursor-pointer font-primary justify-center items-center text-xl"
    >
      <li
        v-for="(item, index) in dataNav"
        :key="index"
        class="py-1 hover:border-yellow-500 hover:border-y-2 hover:text-yellow-500 hover:text-2xl"
      >
        <nuxt-link :to="item.link">{{ item.name }}</nuxt-link>
      </li>
    </ul>

    <div class="flex gap-3">
      <button
        @click="handleAuth"
        class="font-primary w-[10%] sm:w-max sm:block hidden justify-center items-center text-xl py-1 hover:border-yellow-500 hover:border-y-2 hover:text-yellow-500 hover:text-2xl"
      >
        {{ displayButton }}
      </button>
      <button
        v-if="token"
        class="w-10 rounded border-2 hover:border-yellow-400"
      >
        <ic :icon="['fas', 'clipboard']" />
      </button>

      <button @click="handleBars" class="block sm:hidden">
        <ic :icon="['fas', 'bars']" />
      </button>
    </div>
    <ul
      v-if="topbar"
      class="flex flex-1 mr-4 gap-3 cursor-pointer font-primary justify-center items-center text-xl sm:hidden absolute top-[5rem] left-0 bg-red-600 w-full"
    >
      <li
        v-for="(item, index) in dataNav"
        :key="index"
        class="py-1 hover:border-yellow-500 hover:border-y-2 hover:text-yellow-500 hover:text-2xl"
      >
        <nuxt-link :to="item.link">{{ item.name }}</nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<script>
import { dataNav } from '@/utils/navigationData'
import supabase from '@/utils/supabase'

export default {
  data() {
    return {
      dataNav,
      topbar: false,
      token: '',
      login: true,
    }
  },

  methods: {
    async handleAuth() {
      if (this.token) {
        const { error } = await supabase.auth.signOut()
        this.token = ''
      } else {
        this.$router.push('/auth')
      }
    },

    handleBars() {
      this.topbar = !this.topbar
    },
  },

  mounted() {
    const dataToken = JSON.parse(
      localStorage.getItem('sb-bbpezrxaogwdjqzrpsqv-auth-token')
    )
    this.token = dataToken?.access_token
    console.log(this.token)
  },
  computed: {
    displayButton() {
      let namaButton

      if (this.token) {
        namaButton = 'Logout'
      } else {
        namaButton = 'Masuk'
      }

      return namaButton
    },
  },
}
</script>
