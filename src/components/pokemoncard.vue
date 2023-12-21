<!-- PokemonCard.vue -->
<template>
    <div class="pokemon-card">
      <img :src="pokemon.image" :alt="pokemon.name" class="pokemon-image" />
      <div class="pokemon-info">
        <h2>{{ pokemon.name }}</h2>
        <p>Type: {{ pokemon.type }}</p>
        <p>Height: {{ pokemon.height }}</p>
        <p>Weight: {{ pokemon.weight }}</p>
      </div>
    </div>
  </template>

  <script>
  export default {
    props: {
      pokemon: {
        type: Object,
        required: true,
      },
    },
  };
  </script>

  <style scoped>
  /* Ajoutez ici des styles CSS selon vos besoins */
  .pokemon-card {
    border: 1px solid #ddd;
    padding: 10px;
    margin: 10px;
    text-align: center;
  }