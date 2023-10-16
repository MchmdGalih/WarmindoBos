<template>
  <section class="rounded-xl shadow-lg bg-white w-full">
    <div class="pt-3 font-primary w-full">
      <img
        class="object-cover rounded-full w-[200px] h-[200px] m-auto border-4 border-red-300"
        :src="img"
      />
      <h3 class="text-lg font-semibold mt-3 px-3">
        {{ title }}
      </h3>
      <p class="px-3">Rp.{{ price }}</p>
      <button
        class="bg-red-600 border-2 border-red-600 font-semibold text-white rounded-md mx-[0.7rem] mt-2 mb-3 p-2 shadow-xl"
      >
        Pesan Sekarang
      </button>
    </div>
  </section>
</template>
<script>
export default {
  props: {
    img: {
      type: String,
    },
    title: {
      type: String,
    },
    price: {
      type: Number,
    },
  },
  data() {},
}
</script>

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
