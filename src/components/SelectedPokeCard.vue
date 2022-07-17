<script setup lang="ts">
const props = defineProps<{
  selectedPokemon: {
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

}>();




const capitalize = (str: string) => str.charAt(0).toUpperCase() + str.slice(1);
</script>

<template>
  <div class="card modalPokemon">
    <div v-if="selectedPokemon" class="card-body">
      <div class="row">
        <button
          type="button"
          class="close"
          aria-label="Close"
          @click="selectedPokemon = null"
        >
          X
        </button>
        <div class="col-md-4">
          <img
            :src="selectedPokemon.sprites.front_default"
            class="h-24 w-424 rounded-full"
          />
        </div>
        <div class="col-md-8">
          <h3 class="card-title">{{ capitalize(selectedPokemon.name) }}</h3>
          <p class="card-text">
            <span class="font-weight-bold ">Height:</span>
            {{ selectedPokemon.height }}<br />
            <span class="font-weight-bold">Weight:</span>
            {{ selectedPokemon.weight }}<br />
            <span class="font-weight-bold">Abilities:</span>
            {{
              selectedPokemon.abilities
                .map((ability) => ability.ability.name)
                .join(", ")
            }}<br />
            <span class="font-weight-bold">Types:</span>
            {{ selectedPokemon.types.map((type) => type.type.name).join(", ")
            }}<br />
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
