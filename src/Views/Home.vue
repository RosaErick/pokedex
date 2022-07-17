<script setup lang="ts">
import { computed } from "@vue/reactivity";
import { onMounted, reactive, ref } from "vue";

import PokeCard from "../components/PokeCard.vue";
import SelectedPokeCard from "../components/SelectedPokeCard.vue";


const pokemons = reactive(ref());
const search = ref("");
const laoding = ref(true);
const loadingSelectedPokemons = ref(true);
const selectedPokemon = reactive(ref());

const searchResponses = ref("");

const getPokemons = async () => {
  const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=151");
  const data = await response.json();
  pokemons.value = data.results;

  laoding.value = false;
  //add image to each pokemon

  addPokemonImages(pokemons.value);

  console.log(pokemons.value);
};

const addPokemonImages = (pokemons: any) => {
  pokemons.forEach((pokemon: { url: any; image: any }) => {
    fetch(pokemon.url)
      .then((response) => response.json())
      .then((data) => {
        pokemon.image = data.sprites.front_default;
      });
  });
};

const loadMorePokemons = async (event: Event) => {
  const response = await fetch(
    `https://pokeapi.co/api/v2/pokemon?limit=500&offset=${pokemons.value.length}`
  );
  const data = await response.json();
  const newPokemons = data.results;
  pokemons.value = [...pokemons.value, ...newPokemons];

  addPokemonImages(pokemons.value);

  if (newPokemons.length === 0) {
    searchResponses.value = "No more pokemons to load";


  }
  console.log(event);
 
};


const chosenPokemon = (pokemon:any) => {
  loadingSelectedPokemons.value = true;
  fetch(pokemon.url)
    .then((response) => response.json())
    .then((data) => {
      loadingSelectedPokemons.value = false;
      selectedPokemon.value = data;
    });
};

const filterPokemonsComputed = computed(() => {
  if (search.value) {
    return pokemons.value.filter((pokemon: any) => {
      return pokemon.name.toLowerCase().includes(search.value.toLowerCase());
    });
  }
  else { return pokemons.value; }
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

    <SelectedPokeCard
      :loading="loadingSelectedPokemons"
      :selectedPokemon="selectedPokemon"
    
     />

    <ul class="grid grid-cols-1 gap-5">
    <PokeCard
      v-for="pokemon in filterPokemonsComputed"
      :key="pokemon.name"
      :name="pokemon.name"
      :pokeImage="pokemon.image"
      @click="chosenPokemon(pokemon)"

    />
    </ul>
  </div>

  <div class="container">
    <p>{{ searchResponses }}</p>
    <button
      @click="loadMorePokemons"

      class="bg-slate-500 hover:bg-slate-700 text-white font-bold py-2 px-4 rounded"
    >
      Load more pokemons
    </button>
  </div>

  <!-- render search results !--->
</template>

<style></style>
