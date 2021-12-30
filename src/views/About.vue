<template>
  <div>
    <h1>blabla</h1>
    <h3>{{ $route.params.slug }}</h3>
  </div>
</template>

<script>
import { reactive, toRefs } from "@vue/reactivity";
import { useRoute } from "vue-router"

export default {
  setup() {
    const route = useRoute();
    const state = reactive({
      pokemon: null
    })

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then(res => res.json())
      .then(data => {
        console.log(data);
        state.pokemon = data;
      })

      return {...toRefs(state)}
  }
}
</script>

