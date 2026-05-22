<template>
  <div class="bg-gray-50 min-h-screen">

    <!-- HERO -->
    <Section />

    <!-- HOTEL LIST -->
    <div id="hotel-list" class="w-[90%] mx-auto mt-12 ">

      <!-- TITLE -->
      <h1
        class="relative text-3xl sm:text-4xl md:text-5xl font-extrabold text-center
        text-transparent bg-clip-text
        bg-gradient-to-r from-blue-600 via-cyan-400 to-blue-600"
      >
        Popular Hotels

        <span
          class="absolute left-1/2 -translate-x-1/2 bottom-[-10px]
          w-24 h-[4px] bg-gradient-to-r from-blue-500 to-cyan-400 rounded-full blur-sm"
        ></span>
      </h1>

      <p class="mb-6 text-gray-500">
        {{ filteredHotels.length }} Hotels found
      </p>

      <!-- HOTELS -->
      <div class="flex flex-wrap gap-6 justify-center play-title">

        <div
          v-for="item in filteredHotels"
          :key="item.id"
          class="w-[90%] md:w-[45%] lg:w-[23%]"
        >

          <div class="bg-white rounded-2xl overflow-hidden shadow-sm hover:shadow-xl transition group">

            <!-- IMAGE -->
<div class="relative overflow-hidden group">

  <!-- IMAGE -->
  <img
    :src="item.image"
    class="h-[250px] w-full object-cover group-hover:scale-110 transition duration-500"
  />

  <!-- RATING -->
  <div class="absolute top-3 right-3 bg-white/90 px-2 py-1 rounded-full shadow text-sm">
    <i class="bi bi-star-fill text-yellow-400"></i> {{ item.rating }}
  </div>

  <!-- HEART ICON -->
  <button
    class="absolute top-3 left-3 w-10 h-10 rounded-full bg-white/90 flex items-center justify-center shadow-lg
    opacity-0 group-hover:opacity-100
    hover:bg-red-500 hover:text-white
    transition duration-300"
  >
    <i class="bi bi-heart"></i>
  </button>

</div>

            <!-- INFO -->
            <div class="p-4">

              <h2 class="font-semibold text-xl text-gray-700 truncate">
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

              <router-link
                :to="{ path: '/hotels', query: { id: item.id } }"
                class="px-4 py-2 rounded-xl bg-blue-500 text-white hover:bg-blue-700 transition"
              >
                View Hotel
              </router-link>

              </div>

            </div>

          </div>

        </div>

      </div>
    </div>

    <Menufood />
    <Drinkcatary />
    <Service />

  </div>
</template>

<script setup>
import { ref, computed } from "vue"




import Section from "../components/Home/Section.vue"
import Service from "../components/Home/Service.vue"
import Menufood from "../components/Home/Menufood.vue"
import Drinkcatary from "../components/Home/Drinkcatary.vue"

const searchTitle = ref("")

const hotels = ref([
  { id: 1, name: "Single Room", price: 120, rating: 4.8, image: "/assets/image/roomhotel1.png", description: "A beautiful luxury hotel with ocean view..." },
  { id: 2, name: "Honeymoon Room", price: 220, rating: 4.7, image: "/assets/image/roomhotel2.png", description: "Welcome to SkyWayHotel..." },
  { id: 3, name: "Double Room", price: 180, rating: 4.5, image: "/assets/image/roomhotel3.png", description: "Modern rooms with comfort..." },
  { id: 4, name: "Triple Room", price: 250, rating: 4.6, image: "/assets/image/roomhotel4.png", description: "Luxury boutique hotel..." },
  { id: 5, name: "Family Room", price: 280, rating: 4.3, image: "/assets/image/roomhotel5.png", description: "Comfortable beds and WiFi..." },
  { id: 6, name: "Premium Room", price: 300, rating: 4.9, image: "/assets/image/roomhotel6.png", description: "High-end premium stay..." },
  { id: 7, name: "Budget Room", price: 110, rating: 4.2, image: "/assets/image/roomhotel7.png", description: "Affordable and clean..." },
  { id: 8, name: "Ocean View", price: 220, rating: 4.5, image: "/assets/image/roomhotel8.png", description: "Perfect sea view room..." },
])

const filteredHotels = computed(() => {
  return hotels.value.filter(h =>
    h.name.toLowerCase().includes(searchTitle.value.toLowerCase())
  )
})
</script>
<style >
@keyframes bounceIn {
  0% {
    transform: scale(0.5);
    opacity: 0;
  }
  60% {
    transform: scale(1.1);
    opacity: 1;
  }
  100% {
    transform: scale(1);
  }
}

.play-title {
  animation: bounceIn 0.8s ease-out;
}


</style>