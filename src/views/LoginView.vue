<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100 px-4">

    <!-- LOGIN CARD -->
    <div class="w-full max-w-md bg-white rounded-2xl shadow-lg p-8">

      <!-- TITLE -->
      <h1 class="text-3xl font-bold text-center text-blue-600">
        HotelBooker
      </h1>
      <p class="text-center text-gray-500 mt-2">
        Welcome back 👋 Please login
      </p>

      <!-- FORM -->
      <form class="mt-6 space-y-4" @submit.prevent="login">

        <!-- EMAIL -->
        <div>
          <label class="text-sm font-medium text-gray-700">Email</label>
          <input
            v-model="email"
            type="email"
            placeholder="Enter your email"
            class="w-full mt-1 px-4 py-2 border rounded-xl focus:ring-2 focus:ring-blue-400 outline-none"
          />
        </div>

        <!-- PASSWORD -->
        <div>
          <label class="text-sm font-medium text-gray-700">Password</label>
          <input
            v-model="password"
            type="password"
            placeholder="Enter your password"
            class="w-full mt-1 px-4 py-2 border rounded-xl focus:ring-2 focus:ring-blue-400 outline-none"
          />
        </div>

        <!-- FORGOT -->
        <div class="flex justify-end">
          <a href="#" class="text-sm text-blue-500 hover:underline">
            Forgot password?
          </a>
        </div>

        <!-- BUTTON -->
        <button
          type="submit"
          class="w-full bg-blue-500 hover:bg-blue-600 text-white py-2 rounded-xl font-semibold transition"
        >
          Login
        </button>
      </form>

      <!-- FOOTER -->
      <p class="text-center text-sm text-gray-500 mt-6">
        Don't have an account?
        <router-link to="/register" class="text-blue-500 hover:underline">
          Sign up
        </router-link>
      </p>

    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const email = ref('')
const password = ref('')

const login = () => {
  if (!email.value || !password.value) {
    alert('Please fill all fields')
    return
  }

  // fake login
  console.log('Login:', email.value, password.value)

  router.push('/')
}
</script>