<template>
   <router-link
      to="/"
      class="m-3 inline-flex items-center gap-2 px-4 py-2 rounded-xl"
    >
      <i class="bi bi-arrow-left"></i>
      Back
    </router-link>

  <div
    class="min-h-screen flex items-center justify-center bg-gradient-to-br from-slate-50 via-blue-50 to-emerald-50 p-6"
  >
    <div
      class="w-full max-w-6xl grid lg:grid-cols-2 bg-white/70 backdrop-blur-xl shadow-2xl rounded-3xl overflow-hidden border"
    >

      <!-- LEFT SIDE -->
      <div class="p-8 md:p-10 bg-gradient-to-b from-white to-gray-50">

        <!-- TITLE -->
        <div class="mb-6">
          <h1 class="text-3xl font-bold text-gray-800">
            Contact Information
          </h1>

          <p class="text-gray-500 mt-2">
            Get in touch with Sky Way Hotel anytime.
          </p>
        </div>

        

        <!-- INFO -->
        <div class="space-y-4">

          <!-- ADDRESS -->
          <div class="flex items-start gap-4 p-4 bg-white rounded-2xl border shadow-sm">
            <div class="text-2xl">
              <img :src="icons.address" class="w-8 h-8 object-contain mt-1" />
            </div>
            
            <div>
              <h2 class="font-semibold text-gray-800">
                Address
              </h2>

              <p class="text-sm text-gray-500 mt-1">
                Sky Way Hotel, Phnom Penh, Cambodia
              </p>
            </div>
          </div>
          
          <!-- PHONE -->
          <div class="flex items-start gap-4 p-4 bg-white rounded-2xl border shadow-sm">
            <div class="text-2xl">
              <img :src="icons.phone" class="w-8 h-8 object-contain mt-1" />
            </div>
            
            <div>
              <h2 class="font-semibold text-gray-800">
                Phone
              </h2>

              <p class="text-sm text-gray-500 mt-1">
                +855 12 345 678
              </p>
            </div>
          </div>

          <!-- EMAIL -->
          <div class="flex items-start gap-4 p-4 bg-white rounded-2xl border shadow-sm">
            <div class="text-2xl">
              <img :src="icons.email" class="w-8 h-8 object-contain" />
            </div>

            <div>
              <h2 class="font-semibold text-gray-800">
                Email
              </h2>

              <p class="text-sm text-gray-500 mt-1">
                admin@skywayhotel.com
              </p>
            </div>
          </div>

        </div>
        <!-- MAP -->
        <div class="rounded-2xl overflow-hidden border shadow-md mb-6 mt-4">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d125019.28551697!2d104.8226!3d11.5625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3109513f6c2e8f0b%3A0xfb5e6a6c0ba48a99!2sPhnom%20Penh%2C%20Cambodia!5e0!3m2!1sen!2skh!4v1699999999999"
            width="100%"
            height="300"
            style="border: 0"
            allowfullscreen=""
            loading="lazy"
          ></iframe>
        </div>

      </div>

      <!-- RIGHT SIDE -->
      <div class="p-8 md:p-10">

        <!-- HEADER -->
        <div class="mb-6">
          <h1 class="text-3xl font-bold text-gray-800">
            Send Message
          </h1>

          <p class="text-gray-500 mt-2">
            Contact admin directly using the form below.
          </p>
        </div>

        <!-- FORM -->
        <div class="space-y-5">

          <!-- NAME -->
          <div class="flex items-center gap-4 p-4 bg-white rounded-2xl border shadow-sm">

            <input
              v-model="form.name"
              type="text"
              placeholder="Your Name"
              class="flex-1 outline-none text-gray-700 bg-transparent placeholder-gray-400"
            />
          </div>

          <!-- PHONE -->
          <div class="flex items-center gap-4 p-4 bg-white rounded-2xl border shadow-sm">
            

            <input
              v-model="form.phone"
              type="tel"
              placeholder="Your Phone Number"
              class="flex-1 outline-none text-gray-700 bg-transparent placeholder-gray-400"
            />
          </div>

          <!-- EMAIL -->
          <div class="flex items-center gap-4 p-4 bg-white rounded-2xl border shadow-sm">
            

            <input
              v-model="form.email"
              type="email"
              placeholder="Your Email"
              class="flex-1 outline-none text-gray-700 bg-transparent placeholder-gray-400"
            />
          </div>

          <!-- MESSAGE -->
          <div class="flex items-start gap-4 p-4 bg-white rounded-2xl border shadow-sm">
            

            <textarea
              v-model="form.message"
              rows="5"
              placeholder="Your Message to Admin..."
              class="flex-1 outline-none text-gray-700 bg-transparent placeholder-gray-400 resize-none"
            ></textarea>
          </div>

          <!-- SUCCESS -->
          <div
            v-if="submitted"
            class="p-4 rounded-xl bg-emerald-50 border border-emerald-200"
          >
            <p class="text-emerald-700 font-semibold">
              Message sent successfully!
            </p>
          </div>

          <!-- BUTTON -->
          <button
            @click="submitForm"
            :disabled="isLoading"
            class="w-full bg-gradient-to-r from-emerald-500 to-green-600 hover:from-emerald-600 hover:to-green-700 active:scale-95 transition text-white py-3 rounded-xl font-semibold shadow-lg disabled:opacity-60 disabled:cursor-not-allowed flex items-center justify-center gap-2"
          >
            <svg
              v-if="isLoading"
              class="animate-spin w-5 h-5 border-2 border-white border-t-transparent rounded-full"
            ></svg>

            <span v-if="!isLoading">
              Send Message
            </span>

            <span v-else>
              Sending...
            </span>
          </button>

        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"

// icons
const icons = {
  name: "/assets/image/logoName.png",
  phone: "/assets/image/logoPhone.png",
  email: "/assets/image/logoEmail.png",
  address: "/assets/image/logoaddress.png"
}

const form = ref({
  name: "",
  phone: "",
  email: "",
  message: ""
})

const isLoading = ref(false)
const submitted = ref(false)

const submitForm = () => {
  if (!form.value.name || !form.value.email || !form.value.message) {
    alert("Please fill in Name, Email, and Message.")
    return
  }

  isLoading.value = true
  submitted.value = false

  setTimeout(() => {
    isLoading.value = false
    submitted.value = true

    form.value = {
      name: "",
      phone: "",
      email: "",
      message: ""
    }
  }, 2000)
}
</script>