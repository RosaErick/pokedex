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
  console.log(pokemons.value);
  laoding.value = false;
};

const selectPokemon = (pokemon: any) => {
  loadingSelectedPokemons.value = true;
  const response = fetch(pokemon.url).then((response) => response.json());
  response.then((data) => {
    loadingSelectedPokemons.value = false;
    selectedPokemon.value = data;
  });
};

const filterPokemonsComputed = computed(() => {
  return pokemons.value.filter((pokemon: any) => {
    return pokemon.name.toLowerCase().includes(search.value.toLowerCase());
  });
});

onMounted(() => {
  getPokemons();
});
</script>

<template>
  <div class="bg-slate-500">
    <input type="text" v-model="search" />

    <ul class="grid grid-cols-1 gap-5">
      <li
        v-for="pokemon in filterPokemonsComputed"
        :key="pokemon.name"
        @click="selectPokemon(pokemon)"
        class="bg-slate-100 rounded-lg p-2"
      >
        <p class="text-sm text-slate-700">
          {{ pokemon.name }}
        </p>
      </li>
    </ul>
  </div>

  <!-- render search results !--->

  <div class="container pokemons">
    <div
      class="pokemon"
      :key="pokemon.name"
      v-for="pokemon in filterPokemonsComputed"
    >
      <div class="pokemon-name">
        {{ pokemon.name }}
      </div>
      <div class="pokemon-image">
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.name}.png`"
        />
      </div>
      <div class="pokemon-info">
        <button @click="selectPokemon(pokemon)">More info</button>
      </div>
    </div>
  </div>
</template>

<style></style>
