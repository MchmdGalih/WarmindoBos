<template>
  <section class="w-full flex flex-wrap gap-4 justify-center">
    <div
      v-for="item in produk"
      :key="item.id"
      class="w-[300px] flex flex-col p-2 bg-white font-primary mt-[30px] rounded-md"
    >
      <img src="../static/img/mie1.webp" class="object-cover" />

      <h1 class="ml-2 mt-2 text-lg font-bold">{{ item.name }}</h1>
      <p class="ml-2 mt-1">Rp.{{ item.harga }}</p>
      <p class="ml-2 mt-2 h-[150px] tracking-wide text-[14px]">
        {{ item.desc }}
      </p>
      <button
        class="bg-red-600 border-2 border-red-600 ml-1 font-semibold text-white hover:text-slate-400 rounded-md mt-2 p-2 mb- shadow-xl mb-3"
        @click="openModal(item)"
      >
        Pesan
      </button>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    produk: Array,
  },

  methods: {
    openModal(item) {
      this.$emit('openModal', item)
    },
  },
}
</script>
