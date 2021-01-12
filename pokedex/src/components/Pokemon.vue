<template>
  <p v-if="pokemonDetails" @click="sendPokemonToViewer"><img v-bind:src="pokemonDetails.sprites.front_default"/>{{ pokemonDetails.name }}</p>
</template>

<script>
  import axios from 'axios';
  export default {
    name: 'pokemon',
    data() {
      return {
        pokemonDetails: null
      }
    },
    emits: ['pokemon-to-show'],
    mounted() {
      if (this.pokemonurl) {
        // To fetch information about the requested pokemon
        axios.get(this.pokemonurl).then(response => this.pokemonDetails = response.data);
      }
    },
    methods: {
      sendPokemonToViewer() {
        this.$emit('pokemon-to-show', this.pokemonDetails);
      }
    },
    props: ['pokemonurl'],
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
