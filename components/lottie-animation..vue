<template>
  <div>
    <div class="lottie p-4">
      <dotlottie-player
        src="https://lottie.host/a900b907-5d75-4fff-987c-d7cd06732894/7aF7iide9W.json"
        background="transparent"
        speed="1"
        style="width: 500px; height: 500px"
        loop
        autoplay
      ></dotlottie-player>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    const script = document.createElement('script')
    script.src =
      'https://unpkg.com/@dotlottie/player-component@latest/dist/dotlottie-player.js'
    document.head.appendChild(script)
  },
}
</script>

<style></style>
