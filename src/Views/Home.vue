<script setup lang="ts">
import { computed } from "@vue/reactivity";
import { onMounted, reactive, ref } from "vue";

const pokemons = reactive(ref());
const search = ref("");
const laoding = ref(true);
const loadingSelectedPokemons = ref(true);
const selectedPokemon = ref(null);

const getPokemons = async () => {
  const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=151");
  const data = await response.json();
  pokemons.value = data.results;

  laoding.value = false;
  //add image to each pokemon

  pokemons.value.forEach((pokemon: { url: any; image: any }) => {
    fetch(pokemon.url)
      .then((response) => response.json())
      .then((data) => {
        pokemon.image = data.sprites.front_default;
      });
  });

  console.log(pokemons.value);
};

const filterPokemonsComputed = computed(() => {
  if (pokemons.value && search.value) {
    return pokemons.value.filter((pokemon: any) => {
      return pokemon.name.toLowerCase().includes(search.value.toLowerCase());
    });
  }

  return pokemons.value;
});

onMounted(() => {
  getPokemons();
});
</script>

<template>
  <div class="bg-slate-500">
    <input
      type="text"
      v-model="search"
      class="bg-transparent border-none w-full placeholder-gray-500 text-gray-900 rounded-lg py-3 px-4 mb-3 leading-tight focus:outline-none"
    />

    <ul class="grid grid-cols-1 gap-5">
      <li
        v-for="pokemon in filterPokemonsComputed"
        :key="pokemon.name"
        class="bg-slate-100 rounded-lg p-2"
      >
        <img :src="pokemon.image" class="h-24 w-24 rounded-full" />
        <p class="text-sm text-slate-700">
          {{ pokemon.name }}
        </p>
      </li>
    </ul>
  </div>

  <!-- render search results !--->
</template>

<style></style>
