<template>
  <section
    class="flex justify-around mt-4 bg-[#f5f5f5] p-3 drop-shadow-md text-red-600"
  >
    <div
      v-for="(item, i) in cardData"
      :key="i"
      class="w-[400px] h-[200px] rounded-lg text-center font-primary flex flex-col gap-2 justify-center items-center shadow-lg"
    >
      <ic :icon="[item.ic[0], item.ic[1]]" class="text-4xl mb-2" />
      <p class="text-2xl">{{ item.count }}</p>
      <h2 class="font-bold text-3xl">{{ item.title }}</h2>
    </div>
  </section>
</template>

<script>
import { cardData } from '~/utils/navigationData'

export default {
  data() {
    return {
      cardData,
    }
  },
}
</script>

<style></style>
