<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100 px-4">
    
    <div class="w-full max-w-md bg-white rounded-2xl shadow-lg p-8">
      
      <!-- Title -->
      <h1 class="text-3xl font-bold text-center text-gray-800">
        Create Account
      </h1>
      <p class="text-center text-gray-500 mt-2">
        Register to start booking hotels
      </p>

      <!-- Form -->
      <form class="mt-6 space-y-4" @submit.prevent="handleRegister">

        <!-- Name -->
        <div>
          <label class="text-sm font-medium text-gray-700">Full Name</label>
          <input
            v-model="form.name"
            type="text"
            placeholder="Enter your name"
            class="w-full mt-1 px-4 py-2 border rounded-xl focus:ring-2 focus:ring-blue-400 outline-none"
          />
        </div>

        <!-- Email -->
        <div>
          <label class="text-sm font-medium text-gray-700">Email</label>
          <input
            v-model="form.email"
            type="email"
            placeholder="Enter your email"
            class="w-full mt-1 px-4 py-2 border rounded-xl focus:ring-2 focus:ring-blue-400 outline-none"
          />
        </div>

        <!-- Password -->
        <div>
          <label class="text-sm font-medium text-gray-700">Password</label>
          <input
            v-model="form.password"
            type="password"
            placeholder="Enter your password"
            class="w-full mt-1 px-4 py-2 border rounded-xl focus:ring-2 focus:ring-blue-400 outline-none"
          />
        </div>

        <!-- Confirm Password -->
        <div>
          <label class="text-sm font-medium text-gray-700">Confirm Password</label>
          <input
            v-model="form.confirmPassword"
            type="password"
            placeholder="Confirm your password"
            class="w-full mt-1 px-4 py-2 border rounded-xl focus:ring-2 focus:ring-blue-400 outline-none"
          />
        </div>

        <!-- Button -->
        <router-link 
          type="submit"
          class="w-full bg-blue-500 hover:bg-blue-600 text-white py-2 rounded-xl font-semibold transition"
        >
          Register
      </router-link>

      </form>

      <!-- Login link -->
      <p class="text-center text-sm text-gray-500 mt-4">
        Already have an account?
        <router-link to="/login" class="text-blue-500 font-medium">
          Login
        </router-link>
      </p>

    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const form = reactive({
  name: "",
  email: "",
  password: "",
  confirmPassword: ""
});

const handleRegister = () => {
  if (form.password !== form.confirmPassword) {
    alert("Passwords do not match!");
    return;
  }

  console.log("Register Data:", form);

  // 👉 call API here (axios)
};
</script>