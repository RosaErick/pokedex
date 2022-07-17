<script setup lang="ts">
export interface Props {
  name: string;
  pokeImage?: string;
}

const props = defineProps<Props>();

const capitalize = (str: string) => str.charAt(0).toUpperCase() + str.slice(1);
</script>

<template>
  <li class="bg-slate-100 rounded-lg p-2 flex flex-col justify-center items-center" key={name}>
    <img :src="pokeImage" class="h-24 w-24 rounded-full cursor-pointer" />
    <p class="text-sm text-slate-700">
      {{ capitalize(name) }}
    </p>
  </li>
</template>

<style scoped></style>

