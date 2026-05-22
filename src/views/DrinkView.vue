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
  <div class="w-full min-h-screen bg-gray-100 flex justify-center items-center p-4">

    <div class="w-full max-w-5xl bg-white rounded-2xl shadow-lg overflow-hidden grid md:grid-cols-2">

      <!-- IMAGE -->
      <div class="relative">

        <img
          :src="image"
          class="w-full h-[300px] md:h-[500px] object-cover"
        />

        <div
          class="absolute bottom-0 w-full bg-gradient-to-t from-black/70 to-transparent p-5 text-white"
        >

          <h1 class="text-2xl font-bold">
            {{ name }}
          </h1>

          <p class="text-sm opacity-80 mt-1">
            Fresh delicious drink made with premium ingredients
          </p>

          <div class="mt-2 text-yellow-400 font-bold">
            <i class="bi bi-star text-yellow-400"></i>
            4.8 Rating
          </div>

        </div>

      </div>

      <!-- RIGHT SIDE -->
      <div class="p-6 flex flex-col justify-between">

        <div>

          <!-- PRICE -->
          <div class="bg-blue-50 rounded-xl p-4 mb-5">

            <p class="text-gray-500 text-sm">
              Price per item
            </p>

            <h2 class="text-3xl font-bold text-blue-600">
              ${{ price }}
            </h2>

          </div>

          <!-- ROOM -->
          <input
            v-model="roomNumber"
            type="text"
            placeholder="Room Number"
            class="w-full mb-3 p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-400"
          />

          <!-- NAME -->
          <input
            v-model="customerName"
            type="text"
            placeholder="Your Name"
            class="w-full mb-3 p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-400"
          />

          <!-- PHONE -->
          <input
            v-model="phone"
            type="text"
            placeholder="Phone Number"
            class="w-full mb-4 p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-400"
          />

          <!-- ERROR -->
          <div
            v-if="error"
            class="mb-4 p-3 rounded-xl bg-red-50 border border-red-200 text-red-600 font-semibold animate-pulse"
          >
            ⚠️ {{ error }}
          </div>

          <!-- COUNTER -->
          <div class="flex items-center justify-between bg-gray-100 rounded-xl p-4">

            <!-- DEC -->
            <button
              @click="dec"
              class="w-10 h-10 bg-red-500 text-white rounded-xl text-xl font-bold hover:bg-red-600 transition"
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
              class="w-10 h-10 bg-green-500 text-white rounded-xl text-xl font-bold hover:bg-green-600 transition"
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

        </div>

        <!-- ORDER BUTTON -->
        <button
          @click="orderNow"
          class="text-center mt-8 w-full bg-gradient-to-r from-blue-500 to-indigo-600
                text-white py-3 rounded-xl font-bold shadow-lg
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
const roomNumber = ref("");
const customerName = ref("");
const phone = ref("");

// error message
const error = ref("");

// reset
watch(() => route.query.name, () => {
  count.value = 1;
});

// product
const name = computed(() => route.query.name || "Food");

const price = computed(() =>
  Number(route.query.price || 0)
);

const image = computed(() =>
  decodeURIComponent(route.query.image || "")
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
const totalPrice = computed(() =>
  (count.value * price.value).toFixed(2)
);

// order
const orderNow = () => {

  // validation
  if (!roomNumber.value) {
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
      room: roomNumber.value,
      customerName: customerName.value,
      phone: phone.value,
    },
  });
};
</script>