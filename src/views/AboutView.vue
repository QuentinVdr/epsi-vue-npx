<script setup>
import PokemonAbout from '../components/PokemonAbout.vue'
</script>

<template>
  <div class="detail">
    <PokemonAbout :id="this.$route.params.id" />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
