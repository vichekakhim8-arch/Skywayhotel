<template>
  <div>

    <!-- HEADER -->
    <div class="p-4">
      <h1 class="text-2xl font-bold">Hello, Hotels!</h1>

      <!-- 👉 Dynamic count -->
      <p class="text-gray-500 mt-1">
        {{ hotels.length }} hotels found
      </p>
    </div>

    <!-- GRID -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 p-6">

      <div
        v-for="hotel in hotels"
        :key="hotel.id"
        class="bg-white rounded-2xl shadow-md overflow-hidden hover:shadow-xl transition"
      >

        <img :src="hotel.image" class="h-48 w-full object-cover" />

        <div class="p-4">

          <h2 class="text-xl font-bold">
            {{ hotel.name }}
          </h2>

          <p class="text-gray-500 text-sm">
            📍 {{ hotel.location }}
          </p>

          <p class="text-blue-600 font-semibold mt-2">
            ${{ hotel.price }} / night
          </p>

          <p class="text-yellow-500 mt-1">
            ⭐ {{ hotel.rating }}
          </p>

          <router-link to="/HotelDetailView/:id" class="mt-4 w-full bg-blue-500 text-white py-2 rounded-md px-2">
            View Detail
          </router-link>

        </div>

      </div>

    </div>

  </div>
</template>

<script setup>
const hotels = [
  { id: 1, name: "Island Resort", location: "Phuket", price: 120, rating: 4.5, image: "https://images.unsplash.com/photo-1500375592092-40eb2168fd21" },
  { id: 2, name: "Ocean Hotel", location: "Bali", price: 95, rating: 4.2, image: "https://images.unsplash.com/photo-1501117716987-c8e1ecb2103a" },
  { id: 3, name: "Sunset Villa", location: "Maldives", price: 250, rating: 4.9, image: "https://images.unsplash.com/photo-1505693416388-ac5ce068fe85" },
  { id: 4, name: "Beach House", location: "Krabi", price: 180, rating: 4.6, image: "https://images.unsplash.com/photo-1506744038136-46273834b3fb" }
];
</script>