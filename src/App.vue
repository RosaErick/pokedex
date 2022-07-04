<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
</script>

<template>
  <header class="py-5 bg-sky-300">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <nav class="relative z-50 flex justify-between">
        <div class="flex items-center md:gap-x-12">
          <a aria-label="Home" href="#">Pokedex</a>
          <div class="hidden md:flex md:gap-x-6">
            <router-link
              class="inline-block rounded-lg py-1 px-2 text-sm text-slate-700 hover:bg-slate-100 hover:text-slate-900"
              to="/Home"
              >Home</router-link
            >
            <router-link
              class="inline-block rounded-lg py-1 px-2 text-sm text-slate-700 hover:bg-slate-100 hover:text-slate-900"
              to="/about"
              >About</router-link
            >
          </div>
        </div>
      </nav>
    </div>
  </header>

  <!-- CONTENT -->
  <router-view></router-view>
  <!-- -->

  <footer class="mx-auto mt-32 w-full max-w-container px-4 sm:px-6 lg:px-8">
    <div class="border-t border-slate-900/5 py-10">
      <p class="mt-5 text-center text-sm leading-6 text-slate-500">
        Coded by <a>Erick Rosa</a>
      </p>
    </div>
  </footer>
</template>

<style></style>
