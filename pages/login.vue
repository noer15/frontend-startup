<template>
  <div class="h-screen flex justify-center items-center">
    <div
      class="hidden md:block lg:w-1/3 bg-white h-full auth-background rounded-tr-lg rounded-br-lg"
    ></div>

    <div class="w-auto md:w-2/4 lg:w-2/3 flex justify-center items-center">
      <div class="w-full lg:w-1/2 px-10 lg:px-0">
        <h2 class="font-normal mb-6 text-3xl text-white">
          Sign In to Your Account
        </h2>
        <Notification v-if="error" :pesan="error" />
        <form method="post" @submit.prevent="userLogin">
          <div class="mb-6">
            <div class="mb-4">
              <label class="font-normal text-lg text-white block mb-3"
                >Email Address</label
              >
              <input
                v-model="login.email"
                type="email"
                class="auth-form focus:outline-none focus:bg-purple-hover focus:shadow-outline focus:border-purple-hover-stroke focus:text-gray-100"
                placeholder="Write your email address here"
              />
            </div>
          </div>
          <div class="mb-6">
            <div class="mb-4">
              <label class="font-normal text-lg text-white block mb-3"
                >Password</label
              >
              <input
                v-model="login.password"
                type="password"
                class="auth-form focus:outline-none focus:bg-purple-hover focus:shadow-outline focus:border-purple-hover-stroke focus:text-gray-100"
                placeholder="Write your password here"
                @keyup.enter="userLogin"
              />
            </div>
          </div>
          <div class="mb-6">
            <div class="mb-4">
              <button
                type="submit"
                class="inline-flex items-center justify-center w-full bg-orange-button hover:bg-green-button text-white font-semibold px-6 py-4 text-lg rounded-full"
              >
                <svg
                  v-show="loading"
                  class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <circle
                    class="opacity-25"
                    cx="12"
                    cy="12"
                    r="10"
                    stroke="currentColor"
                    stroke-width="4"
                  ></circle>
                  <path
                    class="opacity-75"
                    fill="currentColor"
                    d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
                  ></path>
                </svg>
                Sign In
              </button>
            </div>
          </div>
        </form>
        <div class="text-center">
          <p class="text-white text-md">
            Don't have account?
            <nuxt-link to="/register" class="no-underline text-orange-button"
              >Sign Up</nuxt-link
            >
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  components: {
    Notification,
  },

  layout: 'auth',
  data() {
    return {
      login: {
        email: '',
        password: '',
      },
      error: null,
      loading: false,
    }
  },

  head() {
    return {
      title: 'Login',
    }
  },
  methods: {
    async userLogin() {
      this.loading = true
      try {
        let response = await this.$auth.loginWith('local', { data: this.login })
        this.$auth.setUser(response.data.data)
        console.log(response.data.meta.message)
      } catch (e) {
        this.error = e.response.data.data.errors
        console.log(e.response.data.data.errors)
      }
    },
  },
}
</script>

<style scoped>
.auth-background {
  background-image: url('/sign-in-background.jpg');
  background-position: center;
  background-size: cover;
}
</style>
