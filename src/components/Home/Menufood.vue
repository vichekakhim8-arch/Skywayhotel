<template>
  <div class="w-full flex justify-center bg-gray-100 py-6">
    <div class="w-[92%] md:w-[85%]">

      <h1 class="text-xl sm:text-2xl font-bold mb-4">
        Popular Foods
      </h1>

      <!-- HORIZONTAL SCROLL -->
      <div class="flex gap-4 overflow-x-auto scroll-smooth pb-3">

        <div
          v-for="food in foods"
          :key="food.id"
          @click="goDetail(food)"
          class="cursor-pointer
                 min-w-[140px] sm:min-w-[170px] md:min-w-[200px]
                 h-[140px] sm:h-[170px] md:h-[200px]
                 rounded-2xl overflow-hidden shadow-md
                 shrink-0 bg-white
                 hover:scale-105 transition duration-300"
        >
          <img
            :src="food.image"
            class="w-full h-full object-cover"
            :alt="food.name"
          />
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";

const router = useRouter();

/*
📁 YOUR FILE STRUCTURE MUST BE:
public/
  image/
    buger.png
    pizza.png
    nodal.png
    kako.png
    loklak.png
    pahokang.png
    de.png
    amok.png
*/

const foods = [
  { id: 1, name: "Burger", price: 5, image: "/assets/image/buger.png" },
  { id: 2, name: "Pizza", price: 7, image: "/assets/image/pizza.png" },
  { id: 3, name: "Noodles", price: 4, image: "/assets/image/nodal.png" },
  { id: 4, name: "Somlaor Korko", price: 6, image: "/assets/image/kako.png" },
  { id: 5, name: "Khmer Beef Lok Lak", price: 10, image: "/assets/image/loklak.png" },
  { id: 6, name: "Prahok-Ang", price: 12, image: "/assets/image/pahokang.png" },
  { id: 7, name: "Drink", price: 3, image: "/assets/image/de.png" },
  { id: 8, name: "Amok Fish", price: 9, image: "/assets/image/amok.png" },
];

const goDetail = (food) => {
  router.push({ name: "Fooddetail", query: food });
};
</script>