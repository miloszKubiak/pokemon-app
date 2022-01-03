<template>
  <div class="flex justify-center">
    <div class="w-2/4 flex flex-col justify-center items-center border-4 border-yellow-400 rounded-xl">
      <div class="w-full flex justify-center">
        <input type="text" placeholder="Enter Pokemon here..." class="outline-none mt-10 p-2 border-2 border-blue-500 rounded-xl"
          v-model="text">
      </div>
      <div class="mt-10 p-4 flex flex-wrap justify-center">
        <div class="ml-4 text-2xl text-blue-200"
          v-for="(pokemon, index) in filteredPokemon"
          :key="index"
          >
          <router-link :to="`/about/${urlId[pokemon.name]}`">
            {{ pokemon.name }}
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, reactive, toRefs } from '@vue/reactivity'


export default {
  name: 'Home',
  setup() {

    const state = reactive({
      pokemons: [],
      urlId: {},
      text: "",
      filteredPokemon:computed(() => updatePokemon())
    })

    function updatePokemon() {
      if(!state.text) {
        return[]
      }

      return state.pokemons.filter(pokemon => pokemon.name.includes(state.text))
    }
    
    fetch("https://pokeapi.co/api/v2/pokemon?offset=0")
      .then(res => res.json())
      .then(data => {
        console.log(data)
        state.pokemons = data.results;
        state.urlId = data.results.reduce((accumulator, current, index) =>
        accumulator = {...accumulator, [current.name]:index + 1}
        ,{})
      })

      return {...toRefs(state)}
  }
}
</script>
