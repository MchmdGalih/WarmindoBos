<template>
  <section class="p-2 min-h-screen">
    <div class="p-2 rounded-lg shadow-lg">
      <chart />
    </div>
    <card-dashboard />
  </section>
</template>

<script>
import Chart from '~/components/Chart/Chart.vue'
import CardDashboard from '@/components/Dashboard/CardDashboard.vue'
export default {
  components: { Chart, CardDashboard },
  layout: 'dashboard',
  data() {
    return {}
  },
}
</script>

<style scoped></style>
