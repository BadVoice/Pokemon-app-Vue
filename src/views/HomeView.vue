
<template>
  <div class="w-full flex justify-center">
    <input 
    type="text" placeholder="Enter Pokemon here"
    class="mt-10 p-2 border-vlue-500 border-2"
    v-model="state.text" />

  </div>

  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div class="ml-4 text-2x text-blue-500 "
    v-for="(pokemon, idx) in state.filteredPokemon" :key="idx">
      {{pokemon.name}}
    </div>
  </div>
</template>

<script setup>
import { computed, reactive, toRefs } from "vue"

  const state = reactive({
    pokemons: [],
    urlLookup: {
      
    },
    text: '',
    filteredPokemon: computed(() => updatePokemon()),
  })


  function updatePokemon() {
    if (!state.text) {
      return []
    }

    return state.pokemons.filter((pokemon) => 
    pokemon.name.includes(state.text))
    
  }


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
