<template>
  <div class="about">
    <h1>This is an about page</h1>
    <h3>{{ $route.params.slug}}</h3>
  </div>
</template>

<script setup>
import { reactive, toRefs } from "vue";
import { useRoute } from "vue-router";

  const route = useRoute()
  
  const state = reactive({
    pokemon: null
  })

  fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then((res) => res.json())
      .then((data) => {
        console.log(data)
      })

      
</script>


<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>


