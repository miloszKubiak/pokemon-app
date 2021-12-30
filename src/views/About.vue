<template>
  <div class="">
    <div
      v-if="pokemon"
      class="
        w-2/4
        m-auto
        bg-purple-100
        mt-4
        shadow-2xl
        flex flex-col
        justify-center
      "
    >
      <h3 class="text-2xl font-bold text-center text-green-900 uppercase">
        {{ pokemon.name }}
      </h3>
      <div class="flex justify-center">
        <img :src="pokemon.sprites.front_default" class="w-48" />
        <img :src="pokemon.sprites.back_default" class="w-48" />
      </div>
      <div class="flex flex-col justify-center items-center bg-green-100">
        <div>
          <h3 class="text-center text-yellow-400">Type</h3>
          <div class="" v-for="(type, index) in pokemon.types" :key="index">
            <h5 class="text-red-500">{{ type.type.name }}</h5>
          </div>
        </div>
        <div class="w-2/6">
          <h3 class="text-center">abilities</h3>
          <div
            class="flex items-center"
            v-for="(ability, index) in pokemon.abilities"
            :key="index"
          >
            <h5 class="text-red-500">{{ ability.ability.name }}</h5>
          </div>
        </div>
        <div class="w-2/6">
          <h3 class="text-center">stats</h3>
          <div
            class="flex justify-between bg-blue-200"
            v-for="(stat, index) in pokemon.stats"
            :key="index"
          >
            <h5 class="text-red-800 text-left">{{ stat.stat.name }}</h5>
            <h5 class="text-red-500 text-right">{{ stat.base_stat }}</h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from "@vue/reactivity";
import { useRoute } from "vue-router";

export default {
  setup() {
    const route = useRoute();
    const state = reactive({
      pokemon: null,
    });

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        state.pokemon = data;
      });

    return { ...toRefs(state) };
  },
};
</script>

