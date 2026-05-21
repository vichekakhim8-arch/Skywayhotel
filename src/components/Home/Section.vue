<template>
  <section class="relative h-[80vh] w-full overflow-hidden">

    <!-- BACKGROUND -->
    <div
      class="absolute inset-0 bg-cover bg-center"
      style="background-image: url('/assets/image/bannerSea.png');"
    ></div>

    <!-- OVERLAY -->
    <div class="absolute inset-0 bg-black/40 backdrop-blur-[5px]"></div>

    <!-- CONTENT -->
    <div class="relative z-10 flex flex-col items-center justify-center h-full text-center px-4">

      <h1 class="text-white text-4xl md:text-6xl font-bold mb-4">
        Find Your Perfect Hotel
      </h1>

      <p class="text-white/80 mb-8">
        Search and book your dream stay instantly
      </p>

     <!-- SEARCH BOX -->
<router-link to="/hotels" class="w-full max-w-3xl mx-auto bg-white/10 backdrop-blur-md border border-white/20 rounded-2xl p-3 md:p-4 flex flex-col md:flex-row gap-3">

  <!-- INPUT -->
  <input
    :value="searchTitle"
    @input="$emit('update:searchTitle', $event.target.value)"
    @keyup.enter="$emit('search')"
    type="text"
    placeholder="Search hotel name..."
    class="flex-1 px-4 py-3 rounded-xl bg-white/90 outline-none text-sm md:text-base"
  />

  <!-- BUTTON -->
  <button
    @click="$emit('search')"
    class="w-full md:w-auto px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-xl font-semibold transition active:scale-95"
  >
    Search
  </button>

</router-link>

    </div>

  </section>
</template>

<script setup>
defineProps({
  searchTitle: String
})

defineEmits(['update:searchTitle', 'search'])
</script>