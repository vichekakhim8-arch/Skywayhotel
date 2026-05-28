<template>
  <nav
    class="bg-white/80 backdrop-blur-md sticky top-0 z-50 border-b border-gray-200 shadow-sm"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">

      <!-- NAVBAR -->
      <div class="flex items-center justify-between h-16 lg:h-20">

        <!-- LOGO -->
        <RouterLink
          to="/"
          class="font-extrabold tracking-wide flex items-center text-xl sm:text-2xl lg:text-3xl"
        >
          <span class="text-red-600 text-3xl sm:text-4xl">S</span>

          <span class="bg-gradient-to-r from-blue-600 to-cyan-500 bg-clip-text text-transparent">
            ky
          </span>

          <span class="text-yellow-500">Way</span>

          <span class="text-gray-800">Hotel</span>
        </RouterLink>

        <!-- DESKTOP MENU -->
        <div class="hidden md:flex items-center gap-6 lg:gap-8">

          <RouterLink
            v-for="link in navLinks"
            :key="link.name"
            :to="link.path"
            class="relative group font-medium pb-1 transition duration-300"
            :class="
              isActive(link.path)
                ? 'text-blue-600'
                : 'text-gray-700 hover:text-blue-600'
            "
          >
            {{ link.name }}

            <!-- UNDERLINE -->
            <span
              class="absolute left-0 bottom-0 h-[2px] bg-blue-600 transition-all duration-300"
              :class="
                isActive(link.path)
                  ? 'w-full'
                  : 'w-0 group-hover:w-full'
              "
            ></span>
          </RouterLink>

        </div>

        <!-- DESKTOP BUTTONS -->
        <div class="hidden md:flex items-center gap-3">

          <RouterLink
            to="/login"
            class="px-5 lg:px-6 py-2 rounded-xl border border-blue-600 text-blue-600 hover:bg-blue-600 hover:text-white transition-all duration-300"
          >
            Login
          </RouterLink>

          <RouterLink
            to="/register"
            class="px-5 lg:px-6 py-2 rounded-xl bg-blue-600 text-white hover:bg-blue-700 shadow-md hover:shadow-lg transition-all duration-300"
          >
            Register
          </RouterLink>

        </div>

        <!-- MOBILE BUTTON -->
        <button
          @click="mobileMenu = !mobileMenu"
          class="md:hidden text-3xl text-gray-700"
        >
          ☰
        </button>

      </div>
    </div>

    <!-- MOBILE OVERLAY -->
    <div
      v-if="mobileMenu"
      @click="mobileMenu = false"
      class="fixed inset-0 bg-black/40 z-40 md:hidden"
    ></div>

    <!-- MOBILE MENU -->
    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="translate-x-full"
      enter-to-class="translate-x-0"
      leave-active-class="transition duration-300 ease-in"
      leave-from-class="translate-x-0"
      leave-to-class="translate-x-full"
    >

      <div
        v-if="mobileMenu"
        class="fixed top-0 right-0 w-[80%] sm:w-72 h-screen bg-white shadow-2xl z-50 md:hidden"
      >

        <!-- TOP -->
        <div class="flex items-center justify-between p-5 border-b">

          <h2 class="text-xl font-bold text-blue-600">
            Menu
          </h2>

          <button
            @click="mobileMenu = false"
            class="text-2xl text-gray-700"
          >
            ✕
          </button>

        </div>

        <!-- MOBILE LINKS -->
        <div class="flex flex-col p-5 gap-5">

          <RouterLink
            v-for="link in navLinks"
            :key="link.name"
            :to="link.path"
            @click="mobileMenu = false"
            class="text-lg font-medium transition duration-300"
            :class="
              isActive(link.path)
                ? 'text-blue-600'
                : 'text-gray-700 hover:text-blue-600'
            "
          >
            {{ link.name }}
          </RouterLink>

          <!-- BUTTONS -->
          <div class="border-t pt-5 flex flex-col gap-3">

            <RouterLink
              to="/login"
              class="border border-blue-600 text-blue-600 py-2 rounded-xl text-center hover:bg-blue-600 hover:text-white transition-all duration-300"
            >
              Login
            </RouterLink>

            <RouterLink
              to="/register"
              class="bg-blue-600 text-white py-2 rounded-xl text-center hover:bg-blue-700 transition-all duration-300"
            >
              Register
            </RouterLink>

          </div>

        </div>

      </div>

    </transition>

  </nav>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'

const mobileMenu = ref(false)
const route = useRoute()

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'Hotels', path: '/hotels' },
  { name: 'About', path: '/about' },
  { name: 'Contact', path: '/contact' },
  { name: 'Dashboard', path: '/dashboard' }
]

const isActive = (path) => {
  return route.path === path
}
</script>