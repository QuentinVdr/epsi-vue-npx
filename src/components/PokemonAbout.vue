<template>
  <div class="pokemonDetail" v-if="isLoading">
    <p>loading ...</p>
  </div>
  <div class="pokemonDetail" v-if="handleError">
    <p>{{ handleError.message }}</p>
  </div>
  <div class="pokemonDetail" v-if="pokemon">
    <h1>{{ pokemon.name }}</h1>
    <div v-if="pokemon.sprites">
      <img :src="pokemon.sprites.front_default" :alt="pokemon.name" />
    </div>
    <p v-for="typeInfo in pokemon.types">
      {{ typeInfo.type.name }}
    </p>
    <p v-for="statInfo in pokemon.stats">{{ statInfo.stat.name }}: {{ statInfo.base_stat }}</p>
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
      axios
        .get(apiURL + this.id) // Use this.id instead of id
        .then((result) => {
          console.log(result.data)
          this.pokemon = result.data
          this.isLoading = false
        })
        .catch((error) => {
          this.handleError = error // Assign error to handleError
          this.isLoading = false
        })
    }
  },
  beforeMount() {
    this.getPokemon()
  }
}
</script>
