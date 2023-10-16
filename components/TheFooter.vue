<template>
  <footer class="bg-red-600 py-4 text-center text-white">
    <p>&copy; {{ currentYear }} Warmindo. All rights reserved.</p>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      currentYear: new Date().getFullYear(),
    }
  },
}
</script>
