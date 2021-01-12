<template>
  <div v-if="requestedPokemon">
    <h2>Here is everything about {{ requestedPokemon.name }}</h2>
    <img v-bind:src="requestedPokemon.sprites.front_default"/>
  </div>
  <div v-else>
    Click a pokemon to see more infos about it
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: "PokeViewer",
    data() {
      return {
        requestedPokemon: null,
        pokemonNameCapitalized: null
      }
    },
    props: ['pokemonname'],
    watch: {
      pokemonname: function(newPokemonName) {
        axios.get('https://pokeapi.co/api/v2/pokemon/'+newPokemonName).then(response => this.requestedPokemon = response.data);
        this.pokemonNameCapitalized = this.pokemonname.charAt(0).toUpperCase() + this.pokemonname.slice(1)
      }
    },
  }
</script>

<style scoped>

</style>