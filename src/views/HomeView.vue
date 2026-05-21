<template>
  <div class="bg-gray-50 min-h-screen">

    <!-- HERO SECTION -->
    <Section />

    <!-- HOTEL LIST -->
    <div id="hotel-list" class="w-[90%] mx-auto mt-12">

      <h1
    class="relative text-3xl sm:text-4xl md:text-5xl font-extrabold text-center
           text-transparent bg-clip-text
           bg-gradient-to-r from-blue-600 via-cyan-400 to-blue-600
           tracking-wide"
  >
    Popular Hotels

    <!-- underline glow -->
    <span class="absolute left-1/2 -translate-x-1/2 bottom-[-10px]
                 w-24 h-[4px] bg-gradient-to-r from-blue-500 to-cyan-400
                 rounded-full blur-sm">
    </span>

  </h1>

      <p class="mb-6 text-gray-500">
        {{ filteredHotels.length }} Hotels found
      </p>

      <div class="flex flex-wrap gap-6 justify-center">

        <!-- HOTEL CARD -->
        <div
          v-for="item in filteredHotels"
          :key="item.id"
          class="w-[90%] md:w-[45%] lg:w-[23%]"
        >

          <!-- CARD -->
          <div
            @click="checkLoginAndScroll(item.id)"
            class="group bg-white rounded-2xl overflow-hidden shadow-sm hover:shadow-xl transition block cursor-pointer"
          >

            <!-- IMAGE -->
            <div class="relative overflow-hidden w-full">

              <img
                :src="item.image"
                class="h-[250px] w-full object-cover group-hover:scale-110 transition duration-500"
              />

              <div class="absolute top-3 left-3 bg-white/90 text-xs px-2 py-1 rounded-full shadow opacity-0 group-hover:opacity-100 transition-all duration-300">
                <i class="bi bi-heart text-blue-500 hover:text-blue-700"></i>
              </div>

              <div class="absolute top-3 right-3 bg-white/90 text-xs px-2 py-1 rounded-full shadow">
                ⭐ {{ item.rating }}
              </div>

            </div>

            <!-- CONTENT -->
            <div class="p-4 flex flex-col justify-between">

              <h2 class="font-semibold text-xl truncate text-gray-700">
                {{ item.name }}
              </h2>

              <p class="text-gray-500 text-sm mt-2 line-clamp-2">
                {{ item.description }}
              </p>

              <div class="flex items-center justify-between mt-4">

                <p class="text-blue-600 font-bold text-lg">
                  ${{ item.price }}
                  <span class="text-gray-400 text-sm">/ night</span>
                </p>

                <button
                  @click.stop="checkLoginAndScroll(item.id)"
                  class="px-4 py-2 rounded-xl bg-blue-500 text-white hover:bg-blue-700 transition"
                >
                  View Hotel
                </button>

              </div>

            </div>

          </div>

        </div>

      </div>
    </div>
    <div class="flex justify-center py-10">

  <h1
    class="relative text-3xl sm:text-4xl md:text-5xl font-extrabold text-center
           text-transparent bg-clip-text
           bg-gradient-to-r from-blue-600 via-cyan-400 to-blue-600
           tracking-wide"
  >
    Services

    <!-- underline glow -->
    <span class="absolute left-1/2 -translate-x-1/2 bottom-[-10px]
                 w-24 h-[4px] bg-gradient-to-r from-blue-500 to-cyan-400
                 rounded-full blur-sm">
    </span>

  </h1>

</div>
    <Menufood />
    <Drinkcatary />
    <Service />

  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

import Section from '../components/Home/Section.vue'
import Service from '../components/Home/Service.vue'
import Menufood from '../components/Home/Menufood.vue'
import Drinkcatary from '../components/Home/Drinkcatary.vue'

const router = useRouter()

// 🔐 LOGIN STATE
const isLoggedIn = ref(false)

const searchTitle = ref('')
const searchLocation = ref('')

const hotels = ref([
  { id: 1, name: 'Single Room', price: 120, rating: 4.8, image: '/assets/image/roomhotel1.png', description: 'A beautiful luxury hotel with ocean view...' },
  { id: 2, name: 'Honeymoon room', price: 220, rating: 4.7, image: '/assets/image/roomhotel2.png', description: 'Welcome to SkyWayHotel...' },
  { id: 3, name: 'Double Room', price: 180, rating: 4.5, image: '/assets/image/roomhotel3.png', description: 'Our modern rooms...' },
  { id: 4, name: 'Triple Room', price: 250, rating: 4.6, image: '/assets/image/roomhotel4.png', description: 'Modern boutique hotel...' },
  { id: 5, name: 'Premium Family Room', price: 250, rating: 4.6, image: '/assets/image/roomhotel5.png', description: 'Clean rooms and comfort...' },
  { id: 6, name: 'Family Room', price: 280, rating: 4.3, image: '/assets/image/roomhotel6.png', description: 'Comfortable beds and WiFi...' },
  { id: 7, name: 'Triple Room', price: 110, rating: 4.6, image: '/assets/image/roomhotel7.png', description: 'Near tourist attractions...' },
  { id: 8, name: 'Ocean View Room', price: 220, rating: 4.5, image: '/assets/image/roomhotel8.png', description: 'Perfect for vacations...' },
])

// 🔍 FILTER
const filteredHotels = computed(() => {
  return hotels.value.filter((hotel) =>
    hotel.name.toLowerCase().includes(searchTitle.value.toLowerCase())
  )
})

/* 🚀 LOGIN + SMOOTH SCROLL */
const checkLoginAndScroll = (id) => {

  if (!isLoggedIn.value) {
    alert('⚠️ Please login first to view or book hotel')
    router.push('/login')
    return
  }

  router.push({ name: 'hotel-detail', params: { id } })

  // ✨ SMOOTH SCROLL TO LIST
  setTimeout(() => {
    document.getElementById('hotel-list')?.scrollIntoView({
      behavior: 'smooth',
      block: 'start'
    })
  }, 200)
}
</script>