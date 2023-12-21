
<template>
  <div>
    <h1>Pokemon List</h1>
    <div id="pokemon-list">
      <PokemonCard v-for="(pokemon, index) in data.pokemonList" :key="index" :pokemon="pokemon" />
    </div>
    <div id="demo">
      <ul>
        <li v-for="pokemon in data.pokemonList" :key="pokemon.id">
          {{ pokemon.name }}
          <button @click="fetchData(pokemon.id)">Fetch Pokemon</button>
        </li>
      </ul>
      <div v-if="data.apiData">
        <p>Id: {{ data.apiData.id }}</p>
        <p>Name: {{ data.apiData.name }}</p>
        <img :src="data.apiData.sprites.front_default" alt="pokemon" />
      </div>
      <div v-else>
        <p>Pas de pokémon chargé</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import PokemonCard from './pokemoncard.vue';
import { onMounted } from 'vue';

const apiUrl = "https://pokeapi.co/api/v2/pokemon/";
const config = {};

export default {
  components: {
    PokemonCard,
  },
  setup() {
    const data = {
      apiData: null,
      pokemonList: [],
    };

    const fetchPokemonList = async () => {
      try {
        const response = await axios.get(apiUrl + "?limit=1302");
        data.pokemonList = response.data.results;
      } catch (error) {
        console.error("Erreur de requête Axios:", error);
      }
    };

    const fetchData = async (pokemonId) => {
      try {
        const response = await axios.get(apiUrl + pokemonId, config);
        data.apiData = response.data;
      } catch (error) {
        console.error("Erreur de requête Axios:", error);
      }
    };

    onMounted(() => {
      fetchPokemonList();
    });

    return {
      data,
      fetchData,
    };
  },
};
</script>