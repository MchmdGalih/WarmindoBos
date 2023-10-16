<template>
  <section class="w-full flex flex-col px-4 mb-2">
    <div class="w-full mt-[110px] rounded-md shadow-md bg-[#f5f5f5] pb-4">
      <h1 class="w-full px-4 pt-4 text-3xl font-logo font-bold">
        Menu Makanan
      </h1>
      <CardMenu :produk="makanan" @openModal="openModal" />
    </div>
    <div class="bg-[#f5f5f5] mt-5 rounded-md shadow-md pb-4 mb-3">
      <h1 class="w-full px-4 pt-4 text-3xl font-logo font-bold">
        Menu Minuman
      </h1>
      <CardMenu :produk="minuman" @openModal="openModal" />
    </div>

    <ModalOrder
      :showModal="showModal"
      @closeModal="closeModal"
      :pesanan="pesanan"
      @handlerPesanan="handlerPesanan"
      :minuman="minuman"
      :objectMinuman="objectMinuman"
    />
  </section>
</template>

<script>
import { computed } from 'vue'
import CardMenu from '~/components/CardMenu.vue'
import supabase from '~/utils/supabase'

export default {
  data() {
    return {
      makanan: [],
      minuman: [],
      showModal: false,
      pesanan: {},
      objectMinuman: {},
    }
  },

  methods: {
    async getProdukCard() {
      const { data } = await supabase.from('produk').select()
      const makanan = data.filter((food) => food.kategori === 'makanan')
      const minuman = data.filter((drinks) => drinks.kategori === 'minuman')
      this.makanan = makanan
      this.minuman = minuman
      console.log(minuman, '=======')
    },
    openModal(item) {
      this.showModal = true
      this.pesanan = {
        ...item,
        namaMakanan: item.name,
        namaMinuman: '',
        hargaMakanan: item.harga,
        hargaMinuman: '',
        imgMakanan: item.gambar,
        qtyMakanan: 0,
        qtyMinuman: 0,
        totalHarga: '',
      }
      console.log(this.pesanan)
    },

    handlerPesanan(id) {
      const data = [...this.minuman]
      const item = data.find((i) => i.id === id)
      this.objectMinuman = item
    },

    closeModal() {
      this.showModal = false
    },
  },

  mounted() {
    this.getProdukCard()
    const hargaMinuman = this.minuman.map((item) => item)
    console.log(this.minuman, 'induk')
  },
}
</script>

<style></style>
