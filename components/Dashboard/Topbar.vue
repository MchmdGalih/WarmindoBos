<template>
  <section class="bg-red-600 flex justify-between p-4 items-center">
    <h1 class="font-logo text-2xl font-bold text-white drop-shadow-xl">
      Selamat Datang Admin Tercinta
    </h1>

    <div
      class="bg-[#f5f5f5] flex gap-3 p-2 rounded-md items-center font-secondary font-semibold"
    >
      <ic :icon="['fas', 'user']" />
      <button class="p-1 drop-shadow-2xl">Logout</button>
    </div>
  </section>
</template>

<script>
export default {}
</script>

<style></style>
