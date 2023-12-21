<template>
  <div class="pokemonDetail">
    <h1>This is an detail page {{ id }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true
    }
  }
}
</script>
