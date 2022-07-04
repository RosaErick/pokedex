<script setup lang="ts">
import { ref } from "vue";
</script>

<template>
  <header class="py-5 bg-sky-300">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <nav class="relative z-50 flex justify-between">
        <div class="flex items-center md:gap-x-12">
          <a aria-label="Home" href="#">Pokedex</a>
          <div class="hidden md:flex md:gap-x-6">
            <a
              class="inline-block rounded-lg py-1 px-2 text-sm text-slate-700 hover:bg-slate-100 hover:text-slate-900"
              href="/#features"
              >Home</a
            >
            <a
              class="inline-block rounded-lg py-1 px-2 text-sm text-slate-700 hover:bg-slate-100 hover:text-slate-900"
              href="/#features"
              >About</a
            >
          </div>
        </div>
      </nav>
    </div>
  </header>
</template>

<style scoped></style>
