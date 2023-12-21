<!-- PokemonCard.vue -->
<template>
    <div class="pokemon-card">
      <img :src="pokemon.image" :alt="pokemon.name" class="pokemon-image" />
      <div class="pokemon-info">
        <h2>{{ pokemon.name }}</h2>
        <p>Type: {{ pokemon.type }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps(['pokemon']);
  </script>
  
  <style scoped>
  .pokemon-card {
    border: 1px solid #ddd;
    padding: 10px;
    margin: 10px;
    text-align: center;
  }
  
  .pokemon-image {
    max-width: 100%;
    max-height: 150px;
  }
  
  .pokemon-info {
    margin-top: 10px;
  }
  </style>
  