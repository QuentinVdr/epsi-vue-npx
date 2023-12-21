<template>
  <div class="pokemonDetail">
    <h1>This is an detail page {{ id }}</h1>
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
      console.log('getPokemon')
      axios
        .get(apiURL + this.id) // Use this.id instead of id
        .then((result) => {
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
