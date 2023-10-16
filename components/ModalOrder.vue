<template>
  <section class="relative" v-if="showModal">
    <div class="fixed bg-black/20 w-full h-full left-0 top-0"></div>
    <div
      class="fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 p-2 w-[50%] font-primary px-4 bg-white rounded-lg"
    >
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-3xl font-bold mt-2">Pesanan</h2>
        <span class="cursor-pointer text-3xl" @click="closeModal">&times;</span>
      </div>
      <form class="flex flex-col">
        <h2 class="text-2xl mb-1">Makanan</h2>
        <div class="bg-gray-900 w-[100%] h-1 mb-3"></div>
        <div class="flex justify-between items-center mb-2">
          <img
            src="../static/img/mie1.webp"
            class="w-[50px] h-[50px] object-cover mx-1"
          />
          <div class="flex gap-3">
            <button type="button" @click="pesanan.qtyMakanan--">-</button>
            <p>{{ pesanan.qtyMakanan }}</p>
            <button type="button" @click="pesanan.qtyMakanan++">+</button>
          </div>
        </div>
        <div class="flex justify-between mb-4 items-center">
          <h2 class="p-1 text-[14px]">Harga</h2>
          <p class="text-[14px]">
            Rp. {{ pesanan.hargaMakanan * pesanan.qtyMakanan }}
          </p>
        </div>

        <h2 class="text-2xl mb-1">Minuman</h2>
        <div class="bg-gray-900 w-[100%] h-1 mb-3"></div>
        <div class="flex justify-between items-center mb-2">
          <select v-model="minumanId" @change="handlerPesanan">
            <option value="">Pilih Minuman</option>
            <option v-for="item in minuman" :value="item.id" :key="item.id">
              {{ item.name }}
            </option>
          </select>

          <div class="flex gap-3">
            <button type="button">-</button>
            <p>{{ qtyMinuman }}</p>
            <button type="button" @click="qtyMinuman++">+</button>
          </div>
        </div>
        <div class="flex justify-between mb-4 items-center">
          <h2 class="p-1 text-[14px]">Harga</h2>
          <p class="text-[14px]">
            Rp. {{ objectMinuman.harga ? objectMinuman.harga * qtyMinuman : 0 }}
          </p>
        </div>

        <div class="flex justify-between items-center mb-3">
          <p class="font-bold">Total</p>
          <p class="font-semibold">Rp.3000</p>
        </div>
        <div class="bg-gray-900 w-[100%] h-1 mb-4"></div>
        <button
          type="submit"
          class="bg-red-600 w-[30%] p-1 rounded text-white font-bold mb-4"
        >
          Pesan Sekarang
        </button>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    showModal: Boolean,
    pesanan: Object,
    minuman: Array,
    objectMinuman: Object,
  },
  data() {
    return {
      minumanId: '',
      qtyMinuman: 0,
    }
  },

  computed: {
    displayHargaMinuman() {
      const hargaMinuman = this.minuman.map((harga) => harga.id === 1)
      console.log(hargaMinuman)
    },
  },

  mounted() {
    const hargaMinuman = this.minuman.map((item) => item)
    console.log(this.minuman, 'computed display')
  },

  methods: {
    closeModal() {
      this.$emit('closeModal')
    },

    handlerPesanan() {
      this.$emit('handlerPesanan', this.minumanId)
    },
  },
}
</script>

<style></style>
