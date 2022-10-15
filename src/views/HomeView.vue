
<template>
  <div class="w-full flex justify-center">
    <input type="text" placeholder="Enter Pokemon here"
    class="mt-10 p-2 border-vlue-500 border-2"
    >
  </div>

  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div class="ml-4 text-2x text-blue-500 "
    v-for="(pokemon, idx) in state.pokemons" :key="idx">
      {{pokemon.name}}
    </div>
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
