<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>

  <div class="p-14 ">
    <RouterLink class="flex justify-center text-4xl text-yellow-700"  to="/">Pokemon Picker</RouterLink>
  </div>

  <RouterView />
</template>

<style scoped>

</style>
