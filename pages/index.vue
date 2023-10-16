<script>
import supabase from '@/utils/supabase'

export default {
  data() {
    return {
      // tampung data produk saat fetc api
      produk: [],
    }
  },
  computed: {
    resultMakananFav() {
      const makanan = this.produk.filter((fav) => fav.kategori === 'makanan')
      // const resultMakanan = makanan.filter((fav) => fav.stok <= 10)
      return makanan
    },
  },
  methods: {
    async getProduct() {
      const { data } = await supabase.from('produk').select()
      this.produk = data
    },
  },

  mounted() {
    this.getProduct()

    // const dataToken = JSON.parse(
    //   localStorage.getItem('sb-bbpezrxaogwdjqzrpsqv-auth-token')
    // )
    // if (!dataToken) {
    //   this.$router.push('/auth')
    // }
  },
}
</script>
<template>
  <section class="w-full overflow-x-hidden">
    <HeroSection />
    <section>
      <h1
        class="font-primary text-5xl drop-shadow-xl mt-5 text-red-600 text-center font-bold"
      >
        Tentang Warmindo Kami
      </h1>
      <About />
    </section>

    <section class="mt-5 mb-5 flex flex-col items-center">
      <h1
        class="font-primary text-5xl text-red-600 drop-shadow-xl font-bold mb-5"
      >
        Makanan terfavorit nih bossss!
      </h1>
      <div
        class="w-full py-5 px-4 rounded-lg bg-[#f5f5f5] shadow-xl flex gap-4 pb-4 overflow-x-auto scrollbar"
      >
        <div
          v-for="(item, index) in resultMakananFav"
          :key="index"
          class="w-60"
        >
          <CardFood :img="item.img" :title="item.name" :price="item.harga" />
        </div>
      </div>
    </section>
  </section>
</template>

<style scoped>
.scrollbar::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for IE, Edge and Firefox */
.scrollbar {
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}
</style>
