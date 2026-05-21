<template>
  <div class="bg-gray-50 min-h-screen">

    <!-- HERO SECTION -->
    <Section />

    
    <!-- HOTEL LIST -->
    <div class="w-[90%] mx-auto mt-12">
      <h1 class="text-center font-bold text-3xl py-4">Popular Hotels</h1>

      <p class="  mb-6 text-gray-500">
        {{ filteredHotels.length }} Hotels found
      </p>

      <div class="flex flex-wrap gap-6 justify-center">

        <div
          v-for="item in filteredHotels"
          :key="item.id"
          class="w-[90%] md:w-[45%] lg:w-[23%]"
        >

          <router-link
            :to="{ name: 'hotel-detail', params: { id: item.id } }"
            class="group bg-white rounded-2xl overflow-hidden shadow-sm hover:shadow-xl transition block"
          >

            <!-- IMAGE -->
            <div class="relative group overflow-hidden w-full h-[80%]">

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
            <div class="p-4 flex flex-col justify-between w-full h-[20%]">

              <div>
                <h2 class="font-semibold text-xl truncate text-gray-700">
                  {{ item.name }}
                </h2>

                <p class="text-gray-500 text-sm mt-4 line-clamp-2">
                  {{ item.description }}
                </p>
              </div>

              <div class="flex items-center justify-between mt-5">

                <p class="text-blue-600 font-bold text-lg text-orange-500 hover:text-blue-500">
                  ${{ item.price }}
                  <span class="text-gray-400 text-sm">/ night</span>
                </p>

                <router-link
                  to="/hotels"
                  class="px-4 py-2 rounded-xl bg-blue-500 text-white hover:bg-blue-700 transition"
                >
                  View Hotel
                </router-link>

              </div>

            </div>

          </router-link>

        </div>

      </div>
    </div>

    <Menufood />
    <Drinkcatary />
    <Service />

  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import Section from '../components/Home/Section.vue'
import Service from '../components/Home/Service.vue'
import Menufood from '../components/Home/Menufood.vue'
import Drinkcatary from '../components/Home/Drinkcatary.vue'

const searchTitle = ref('')
const searchLocation = ref('')

const hotels = ref([
  {
    id: 1,
    name: 'Single Room',
    price: 120,
    rating: 4.8,
    image: '/assets/image/roomhotel1.png',
    description: 'A beautiful luxury hotel with ocean view...',
  },
  {
    id: 2,
    name: 'Honeymoon room',
    price: 220,
    rating: 4.7,
    image: '/assets/image/roomhotel2.png',
    description: 'Welcome to SkyWayHotel...',
  },
  {
    id: 3,
    name: 'Double Room',
    price: 180,
    rating: 4.5,
    image: '/assets/image/roomhotel3.png',
    description: 'Our modern rooms...',
  },
  {
    id: 4,
    name: 'Triple Room',
    price: 250,
    rating: 4.6,
    image: '/assets/image/roomhotel4.png',
    description: 'Modern boutique hotel...',
  },
  {
    id: 5,
    name: 'Premium Family Rooml',
    price: 250,
    rating: 4.6,
    image: '/assets/image/roomhotel5.png',
    description: 'The hotel provides clean rooms...',
  },
  {
    id: 6,
    name: 'Family Room',
    price: 280,
    rating: 4.3,
    image: '/assets/image/roomhotel6.png',
    description: 'Comfortable beds and WiFi...',
  },
  {
    id: 7,
    name: 'Triple Room',
    price: 110,
    rating: 4.6,
    image: '/assets/image/roomhotel7.png',
    description: 'Near tourist attractions...',
  },
  {
    id: 8,
    name: 'Ocean View Room',
    price: 220,
    rating: 4.5,
    image: '/assets/image/roomhotel8.png',
    description: 'Perfect for vacations...',
  },
])

const filteredHotels = computed(() => {
  return hotels.value.filter((hotel) => {
    const matchTitle = (hotel.name ?? "")
      .toLowerCase()
      .includes((searchTitle.value ?? "").toLowerCase())

    const matchLocation = (hotel.location ?? "")
      .toLowerCase()
      .includes((searchLocation.value ?? "").toLowerCase())

    return matchTitle && matchLocation
  })
})
</script>