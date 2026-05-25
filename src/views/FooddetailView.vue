<template>
  <!-- BACK BUTTON -->
  <router-link
    to="/"
    class="m-3 inline-flex items-center gap-2 px-4 py-2 rounded-xl"
  >
    <i class="bi bi-arrow-left"></i>
    Back
  </router-link>

  <!-- MAIN -->
  <div
    class="w-full min-h-screen bg-gradient-to-br from-blue-50 via-white to-indigo-50 flex justify-center items-center p-4"
  >
    <div
      class="w-full max-w-5xl bg-white rounded-3xl shadow-2xl overflow-hidden grid md:grid-cols-2"
    >

      <!-- IMAGE -->
      <div class="relative">
        <img
          :src="image"
          class="w-full h-[350px] md:h-[500px] object-cover"
          :alt="name"
        />

        <div
          class="absolute inset-0 bg-gradient-to-t from-black/70 via-black/20 to-transparent"
        ></div>

        <div class="absolute bottom-0 w-full p-6 text-white">
          <h1 class="text-3xl font-bold">
            {{ name }}
          </h1>

          <p class="text-sm opacity-80 mt-1">
            Fresh drink made with premium ingredients 🍹
          </p>

          <div class="mt-2 text-yellow-300 font-bold">
            <i class="bi bi-star text-yellow-400"></i>
            4.8 Rating
          </div>
        </div>
      </div>

      <!-- RIGHT SIDE -->
      <div class="p-6 flex flex-col justify-between">

        <!-- PRICE -->
        <div class="bg-blue-50 rounded-2xl p-5 mb-5 shadow-sm">
          <p class="text-gray-500 text-sm">
            Price per item
          </p>

          <h2 class="text-4xl font-bold text-blue-600">
            ${{ price }}
          </h2>
        </div>

        <!-- FORM -->
        <div class="space-y-4 mb-5">

          <!-- ROOM -->
          <input
            v-model="room"
            type="text"
            placeholder="Room Number"
            class="w-full p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-400"
          />

          <!-- NAME -->
          <input
            v-model="customerName"
            type="text"
            placeholder="Your Name"
            class="w-full p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-400"
          />

          <!-- PHONE -->
          <input
            v-model="phone"
            type="text"
            placeholder="Phone Number"
            class="w-full p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-400"
          />

        </div>

        <!-- ERROR -->
        <p
          v-if="error"
          class="text-red-500 font-semibold m-3 bg-red-50 py-3 px-4 rounded-xl"
        >
          ⚠️ {{ error }}
        </p>

        <!-- COUNTER -->
        <div
          class="flex items-center justify-between bg-gray-100 rounded-2xl p-4 shadow-sm"
        >

          <!-- DEC -->
          <button
            @click="dec"
            class="w-11 h-11 bg-red-500 text-white rounded-xl text-xl font-bold hover:bg-red-600 transition"
          >
            -
          </button>

          <!-- COUNT -->
          <span class="text-2xl font-bold">
            {{ count }}
          </span>

          <!-- INC -->
          <button
            @click="inc"
            class="w-11 h-11 bg-green-500 text-white rounded-xl text-xl font-bold hover:bg-green-600 transition"
          >
            +
          </button>

        </div>

        <!-- TOTAL -->
        <div class="mt-6 space-y-3 text-lg">

          <div class="flex justify-between">
            <span class="text-gray-600">
              Total Items
            </span>

            <span class="font-bold">
              {{ count }}
            </span>
          </div>

          <div class="flex justify-between">
            <span class="text-gray-600">
              Total Price
            </span>

            <span class="font-bold text-green-600">
              ${{ totalPrice }}
            </span>
          </div>

        </div>

        <!-- ORDER BUTTON -->
        <button
          @click="orderNow"
          class="mt-6 w-full text-center bg-gradient-to-r from-blue-500 to-indigo-600
                text-white py-3 rounded-2xl font-bold shadow-lg
                hover:scale-105 transition"
        >
          Order Now
        </button>

      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();

const count = ref(1);

// form
const room = ref("");
const customerName = ref("");
const phone = ref("");

const error = ref("");

// reset count when product changes
watch(() => route.query.id, () => {
  count.value = 1;
});

// product info
const name = computed(() => route.query.name || "Drink");

const price = computed(() =>
  Number(route.query.price || 0)
);

const image = computed(() =>
  route.query.image || ""
);

// counter
const inc = () => {
  count.value++;
};

const dec = () => {
  if (count.value > 1) {
    count.value--;
  }
};

// total
const totalPrice = computed(() => {
  return count.value * price.value;
});

// order
const orderNow = () => {

  // validation
  if (!room.value) {
    error.value = "Please enter room number";
    return;
  }

  if (!customerName.value) {
    error.value = "Please enter your name";
    return;
  }

  if (!phone.value) {
    error.value = "Please enter phone number";
    return;
  }

  // clear error
  error.value = "";

  // go payment page
  router.push({
    path: "/payment",

    query: {
      name: name.value,
      image: image.value,
      price: price.value,
      qty: count.value,
      total: totalPrice.value,
      room: room.value,
      customerName: customerName.value,
      phone: phone.value,
    },
  });
};
</script>