<template>
  <form
    @submit.prevent="handleLogin"
    class="flex flex-col p-5 text-black font-bold w-full"
  >
    <h2 class="drop-shadow-xl mb-5 text-3xl">Masuk dulu dong guys!</h2>
    <label class="text-lg">Email</label>
    <input
      id="email"
      type="email"
      class="form-control p-2 mt-2"
      placeholder="Masukan Email Anda"
      v-model="formData.email"
    />
    <label class="text-lg mt-2">Password</label>
    <input
      id="password"
      type="password"
      class="form-control p-2 mt-2"
      placeholder="Masukan Password Anda"
      v-model="formData.password"
    />
    <p
      class="mt-4 text-blue-900 cursor-pointer text-sm"
      @click="handleRegister"
    >
      Belum punya akun kan ka?
    </p>
    <button class="w-full bg-white font-bold mt-2 rounded-md p-2" type="submit">
      Masuk
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        email: '',
        password: '',
      },
    }
  },

  methods: {
    handleRegister() {
      this.$emit('register')
    },

    handleLogin() {
      this.$emit('formSubmit', this.formData)
    },
  },
}
</script>
