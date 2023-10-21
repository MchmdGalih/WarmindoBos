<template>
  <section>
    <div class="flex">
      <side-bar />
      <div class="w-full">
        <topbar />
        <Nuxt />
      </div>
    </div>
  </section>
</template>

<script>
import Topbar from '~/components/Dashboard/Topbar.vue'
import SideBar from '~/components/Dashboard/SideBar.vue'
export default {
  components: { Topbar, SideBar },
  name: 'dashboard',
}
</script>

<style></style>
