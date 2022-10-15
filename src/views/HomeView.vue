
<template>
  <div class="home">
    <h3>Hello world</h3>
    {{stateAsRefs.pokemons}}
  </div>
</template>

<script setup>
import { reactive, toRefs } from "vue"

  const state = reactive({
    pokemons: [],
    urlLookup: {
      
    }
  })


  fetch("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
    .then((res) => res.json())
    .then((data) => {
      console.log(data)
      state.pokemons = data.results;
      state.urlLookup = data.results.reduce((acc, cur, idx) => 
        acc = {...acc, [cur.name]:idx+1}
      ,{})
      
    })

    const stateAsRefs = toRefs(state)
</script>
