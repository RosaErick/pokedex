<script setup lang="ts">
import type { Ref } from "vue";

const props = defineProps<{
  selectedPokemon?: {
    name: string;

    sprites: {
      front_default: string;
    };
    height: number;
    weight: number;
    abilities: {
      ability: {
        name: string;
        url: string;
      };
    }[];

    types: {
      type: {
        name: string;
        url: string;
      };
    }[];
  };
  loading: boolean;
  display: boolean;
}>();

const capitalize = (str: string) => str.charAt(0).toUpperCase() + str.slice(1);
</script>

<template>
  <div
    v-if="display"
    class="card modalPokemon md:flex bg-slate-100 rounded-xl p-10 md:p-0 dark:bg-slate-800"
  >
    <button
      type="button"
      class="close"
      aria-label="Close"
      @click="display = false"
    >
      X
    </button>

    <img
      :src="selectedPokemon.sprites.front_default"
      class="w-24 h-24 md:w-48 md:h-auto md:rounded-none rounded-full mx-auto"
    />

    <div class="col-md-8 md:h-auto">
      <ul class="card-info flex flex-col p-5">
        <h3 class="card-title pb-1">{{ capitalize(selectedPokemon.name) }}</h3>
        <li class="font-weight-bold">Height: {{ selectedPokemon.height }}</li>

        <li class="font-weight-bold">Weight: {{ selectedPokemon.weight }}</li>

        <li class="font-weight-bold">
          Abilities:
          {{
            selectedPokemon.abilities
              .map((ability) => ability.ability.name)
              .join(", ")
          }}
        </li>

        <li class="font-weight-bold">
          Types:
          {{ selectedPokemon.types.map((type) => type.type.name).join(", ") }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
