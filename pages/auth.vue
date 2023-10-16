<template>
  <section
    class="card-container w-full min-h-screen flex justify-center items-center font-secondary"
  >
    <div
      class="bg-gradient-to-r from-red-100 to-red-400 rounded-md flex items-center shadow-xl"
    >
      <LoginInput
        @formSubmit="formSubmit"
        @register="handleRegister"
        v-if="!register"
      />
      <RegisterInput
        @register="handleRegister"
        v-else
        @formSubmit="formSubmit"
      />
      <lottie-animation />
    </div>
  </section>
</template>

<script>
import LoginInput from '~/components/Auth/LoginInput.vue'
import RegisterInput from '~/components/Auth/RegisterInput.vue'
import { createClient } from '@supabase/supabase-js'

const supabaseUrl = process.env.SUPABASE_URL
const supabaseKey = process.env.SUPABASE_KEY
const supabase = createClient(supabaseUrl, supabaseKey)
export default {
  components: { LoginInput, RegisterInput },
  name: 'auth',
  layout: 'empty',

  data() {
    return {
      register: false,
    }
  },

  methods: {
    handleRegister() {
      this.register = !this.register
    },
    async formSubmit(formData) {
      if (this.register) {
        const { data, error } = await supabase.auth.signUp({
          email: formData.email,
          password: formData.password,
          options: {
            data: {
              username: formData.username,
            },
          },
        })
        console.log(data, '--> register')
      }
      const { data, error } = await supabase.auth.signInWithPassword({
        email: formData.email,
        password: formData.password,
      })
      this.$router.push('/')
      console.log(data, 'login')
    },
  },
}
</script>
