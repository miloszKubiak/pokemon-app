<template>
  <div>
    <h1>hello</h1>
    {{ pokemons }}
  </div>
</template>

<script>
import { reactive, toRefs } from '@vue/reactivity'


export default {
  name: 'Home',
  setup() {

    const state = reactive({
      pokemons: [],
      urlId: {}
    })
    
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
