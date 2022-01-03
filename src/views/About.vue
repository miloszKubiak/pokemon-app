<template>
  <div class="flex justify-center">
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
        rounded-xl
      "
    >
      <h3 class="text-2xl mt-4 font-bold text-center uppercase">
        {{ pokemon.name }}
      </h3>
      <div class="flex justify-around">
        <img :src="pokemon.sprites.front_default" class="w-48" />
        <img :src="pokemon.sprites.back_default" class="w-48" />
      </div>
      <div class="flex flex-col justify-center items-center bg-purple-200 rounded-b-xl">
        <div>
          <h3 class="text-center font-bold mt-4">Type</h3>
          <div class="" v-for="(type, index) in pokemon.types" :key="index">
            <h5 class="text-center">{{ type.type.name }}</h5>
          </div>
        </div>
        <div class="w-2/6 flex flex-col items-center">
          <h3 class="text-center font-bold mt-4">Abilities</h3>
          <div
            class=""
            v-for="(ability, index) in pokemon.abilities"
            :key="index"
          >
            <h5 class="text-center">{{ ability.ability.name }}</h5>
          </div>
        </div>
        <div class="w-2/6">
          <h3 class="text-center mt-4 font-bold">Stats</h3>
          <div
            class="flex justify-between"
            v-for="(stat, index) in pokemon.stats"
            :key="index"
          >
            <h5 class="text-left">{{ stat.stat.name }}</h5>
            <h5 class="text-right">{{ stat.base_stat }}</h5>
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

