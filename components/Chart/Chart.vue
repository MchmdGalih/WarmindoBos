<template>
  <div class="p-2 border bg-[#f4f4f4]">
    <label class="block mb-2 font-bold"> Order Perhari </label>

    <client-only>
      <BarChart :data="chartData" />
    </client-only>
  </div>
</template>

<script>
export default {
  props: {
    penilaian: {
      type: Object,
      required: true,
    },
  },
  computed: {
    chartData() {
      return {
        labels: [
          'Senin',
          'Selasa',
          'Rabu',
          'Kamis',
          'Jumat',
          'Sabtu',
          'Minggu',
        ],
        datasets: [
          {
            label: '',
            data: [2, 1, 16, 3, 2, 7, 8],
            backgroundColor: 'rgba(230, 23, 23, 0.92)',
            borderWidth: 2,
          },
        ],
      }
    },
  },
}
</script>
