<template>
  <section class="w-full p-3">
    <div class="w-full flex justify-between px-2 mb-2 items-center">
      <button class="rounded border-2 border-red-600 p-2 font-semibold shadow-">
        Tambah Produk
      </button>
      <input
        type="text"
        name="search"
        id="price"
        v-model="searchProduk"
        class="block rounded-md border-0 text-gray-900 ring-1 p-2 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset"
        placeholder="Search"
      />
    </div>
    <div class="w-full bg-white rounded shadow-sm border">
      <h1 class="text-lg font-bold p-2">Produk Management</h1>
      <div class="inline-block w-full overflow-x-auto">
        <table class="w-full table-auto text-left text-sm font-light py-2">
          <thead
            class="sticky -z-1 top-0 bg-slate-300 font-medium border-neutral-500"
          >
            <tr>
              <th scope="col" class="px-6 py-4">No.</th>
              <th scope="col" class="px-6 py-4">Nama Produk</th>
              <th scope="col" class="px-6 py-4">Harga</th>
              <th scope="col" class="px-6 py-4">Stok</th>
              <th scope="col" class="px-6 py-4">Gambar</th>
              <th scope="col" class="px-6 py-4">Kategori</th>
              <th scope="col" class="px-6 py-4">Deskripsi</th>
              <th scope="col" class="px-6 py-4">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(produk, index) in searchResult" :key="produk.id">
              <td class="whitespace-nowrap px-6 py-4 font-medium">
                {{ index + 1 }}
              </td>
              <td class="whitespace-nowrap px-6 py-4">{{ produk.name }}</td>
              <td class="whitespace-nowrap px-6 py-4">{{ produk.harga }}</td>
              <td class="whitespace-nowrap px-6 py-4">{{ produk.stok }}</td>
              <td class="whitespace-nowrap px-6 py-4">{{ produk.gambar }}</td>
              <td class="whitespace-nowrap px-6 py-4">
                {{ produk.kategori }}
              </td>
              <td class="px-6 py-4">{{ produk.desc }}</td>
              <td class="whitespace-nowrap px-6 py-4 flex items-center gap-2">
                <button class="btn btn-info">Edit</button>
                <button class="btn btn-danger">Hapus</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>
</template>

<script>
import supabase from '~/utils/supabase'
export default {
  layout: 'dashboard',
  data() {
    return {
      produks: [],
      searchProduk: '',
    }
  },
  computed: {
    searchResult() {
      if (this.searchProduk) {
        const searchList = this.searchProduk.toLowerCase().trim()
        return this.produks.filter((produk) =>
          produk.name.toLowerCase().includes(searchList)
        )
      } else {
        return this.produks
      }
    },
  },
  methods: {
    async getProduk() {
      const { data } = await supabase.from('produk').select()
      this.produks = data
      console.log('-->', this.produk)
    },
  },

  mounted() {
    this.getProduk()
  },
}
</script>

<style></style>
