<template>
  <section
    class="bg-red-600 min-h-screen flex flex-col w-[200px] font-secondary"
  >
    <div>
      <img
        src="../../static/img/logo.png"
        class="w-[100px] h-[80px] object-cover mb-3"
      />
    </div>

    <div class="w-full h-[2px] shadow-sm bg-white mb-4"></div>

    <div class="w-full flex justify-between items-center mb-4 px-2">
      <nuxt-link to="/admin" class="text-white font-secondary drop-shadow-md"
        >Dashboard</nuxt-link
      >
      <nuxt-link to="/admin">
        <ic :icon="['fas', 'house']" style="color: #ffffff"
      /></nuxt-link>
    </div>

    <div class="flex justify-between items-center mb-4 px-2">
      <nuxt-link
        to="/admin/users"
        class="text-white font-secondary drop-shadow-md"
        >Users</nuxt-link
      >
      <nuxt-link to="/admin/users">
        <ic :icon="['fas', 'users']" style="color: #ffffff" />
      </nuxt-link>
    </div>

    <div class="flex justify-between items-center px-2">
      <nuxt-link
        to="/admin/product"
        class="text-white font-secondary drop-shadow-md"
        >Product</nuxt-link
      >
      <nuxt-link to="/admin/product">
        <ic :icon="['fas', 'store']" style="color: #ffffff" />
      </nuxt-link>
    </div>
  </section>
</template>

<script>
export default {}
</script>

<style></style>
