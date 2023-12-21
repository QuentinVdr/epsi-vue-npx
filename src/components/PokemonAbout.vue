<template>
  <div>
    <div v-if="isLoading" class="pokemonDetail">
      <p>Loading...</p>
    </div>
    <div v-if="handleError" class="pokemonDetail">
      <p>Error: {{ handleError.message }}</p>
    </div>
    <div v-if="pokemon" class="pokemonDetail">
      <h1>{{ pokemon.name }}</h1>
      <div v-if="pokemon.sprites">
        <img :src="pokemon.sprites.front_default" :alt="pokemon.name" />
      </div>
      <p v-for="typeInfo in pokemon.types" :key="typeInfo.slot">
        {{ typeInfo.type.name }}
      </p>
      <PokemonStatChart :pokemonStats="pokemon.stats" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'

const apiURL = 'https://pokeapi.co/api/v2/pokemon/'

export default {
  props: {
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      isLoading: true,
      handleError: null,
      pokemon: {}
    }
  },
  methods: {
    async getPokemon() {
      try {
        const result = await axios.get(apiURL + this.id)
        this.pokemon = result.data
      } catch (error) {
        this.handleError = error
      } finally {
        this.isLoading = false
      }
    }
  },
  beforeMount() {
    this.getPokemon()
  }
}
</script>
