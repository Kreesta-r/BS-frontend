<script setup lang="ts">
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const rememberMe = ref(false)

const handleTestLogin = async () => {
  try {
    const response = await fetch('http://localhost:3000/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        email: email.value,
        password: password.value
      })
    });

    if (response.ok) {
      const data = await response.json();
      alert(`Login successful! Role: ${data.role}`);
    } else {
      const errorData = await response.json();
      alert(`Login failed: ${errorData.message}`);
    }
  } catch (error) {
    console.error('Login error:', error);
    alert('An error occurred during login');
  }
}
</script>

<template>
  <div class="min-h-screen w-full flex flex-col lg:flex-row font-sans text-gray-800 bg-white">
    
    <!-- Left -->
    <div class="hidden lg:flex w-full lg:w-[46%] bg-[#F9F3FF] flex-col items-center justify-center py-10 px-6 xl:px-10 relative">
      
      <!-- Container to left-align Logo with the Image -->
      <div class="w-full max-w-[626px] flex flex-col items-start -mt-10">
        
        <!-- Logo Container -->
        <img 
          src="./assets/logo.png" 
          alt="Logo" 
          class="w-[198px] h-[97px] object-contain mb-6 -ml-2" 
        />

        <!-- Main Image -->
        <img 
          src="./assets/hero.png" 
          alt="Group of friends" 
          class="w-full h-[auto] aspect-[626/417] object-cover rounded-[20px]"
        />
        
        <!-- Text under image -->
        <div class="mt-6 w-full text-center space-y-[4px]">
          <h2 class="text-[#652d90] font-bold text-[22px]" style="font-family: Georgia, serif;">Team Achieve</h2>
          <p class="text-gray-500 font-medium text-[15px]" style="font-family: Georgia, serif;">Your perfect solution for funding your desires</p>
        </div>

      </div>
    </div>

    <!-- Right, Form Layout -->
    <div class="w-full lg:w-[54%] flex flex-col items-center justify-center p-6 sm:p-12 md:p-8 overflow-y-auto bg-white min-h-screen lg:min-h-0">
      
      <!-- Form Container -->
      <div class="w-full max-w-[620px] flex flex-col gap-[24px]">
        
        <!-- Mobile Logo -->
        <div class="flex lg:hidden flex-col items-center">
          <img src="./assets/logo.png" alt="Logo" class="w-[160px] sm:w-[198px] h-auto object-contain" />
        </div>

        <!-- Heading -->
        <div class="text-center flex flex-col gap-[8px]">
          <h1 class="text-[28px] font-bold text-[#652d90]" style="font-family: Georgia, serif;">Welcome Back</h1>
          <p class="text-gray-500 text-[14px]">Enter your email address and password to access your account.</p>
        </div>

        <!-- Form -->
        <form @submit.prevent="handleLogin" class="flex flex-col gap-[28px]">
          
          <div class="flex flex-col gap-[6px]">
            <label for="email" class="block text-[13px] text-gray-700 font-medium text-left">
              Email Address <span class="text-red-500">*</span>
            </label>
            <input 
              id="email" 
              v-model="email" 
              type="email" 
              placeholder="Enter your email" 
              class="w-full px-[16px] py-[16px] rounded-[5px] border border-[#d1d5db] focus:outline-none focus:ring-1 focus:ring-[#652d90] focus:border-[#652d90] text-[14px] transition-colors placeholder:text-[#9ca3af] bg-transparent"
              required
            >
          </div>
          <div class="flex flex-col gap-[6px]">
            <label for="password" class="block text-[13px] text-gray-700 font-medium text-left">
              Password <span class="text-red-500">*</span>
            </label>
            <div class="flex items-stretch w-full rounded-[5px] border border-[#d1d5db] focus-within:ring-1 focus-within:ring-[#652d90] focus-within:border-[#652d90] transition-colors bg-transparent">
              <input 
                id="password" 
                v-model="password" 
                type="password" 
                placeholder="Enter your password" 
                class="flex-grow pl-[16px] py-[16px] outline-none text-[14px] bg-transparent placeholder:text-[#9ca3af]"
                required
              >
              <div class="flex items-center justify-center border-l border-[#d1d5db] px-[16px] cursor-pointer text-[#9ca3af] hover:text-gray-500 transition-colors">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" class="w-[20px] h-[20px]">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" />
                  <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
              </div>
            </div>
          </div>

          <div class="flex items-center justify-between -mt-[8px]">
            <label class="flex items-center gap-[8px] cursor-pointer group">
              <input 
                type="checkbox" 
                v-model="rememberMe" 
                class="w-[16px] h-[16px] rounded-[3px] border-gray-300 text-[#652d90] focus:ring-[#652d90]"
              >
              <span class="text-[13px] text-gray-500 group-hover:text-gray-700 transition-colors">Remember me</span>
            </label>
            <a href="#" class="text-[13px] text-[#652d90] hover:underline font-semibold">Forgot Password?</a>
          </div>

          <button 
            type="submit" 
            class="w-full bg-[#652d90] hover:bg-[#522475] text-white py-[16px] rounded-[5px] font-semibold text-[15px] transition-colors shadow-sm"
          >
            Sign in
          </button>
        </form>

        <!-- Footer -->
        <p class="text-center text-[14px] text-gray-600">
          Don't have an account? 
          <a href="#" class="text-[#652d90] font-semibold hover:underline ml-1">Sign up</a>
        </p>
      </div>

    </div>
  </div>
</template>

<style>
/* Reset */
body, html, #app {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background-color: white;
}
</style>
