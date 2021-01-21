<template>
  <span v-if="pokemonDetails">
    <span @click="sendPokemonToViewer">
      <img v-bind:src="pokemonDetails.sprites.front_default"/>
      {{ pokemonDetails.name }}
    </span>
    <button class="ml-1" @click="sendPokemonToCurrentParty">Add to party</button>
  </span>
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
    emits: ['pokemon-to-show', 'pokemon-to-add'],
    mounted() {
      if (this.pokemonurl) {
        // To fetch information about the requested pokemon
        axios.get(this.pokemonurl).then(response => this.pokemonDetails = response.data);
      }
    },
    methods: {
      sendPokemonToViewer() {
        this.$emit('pokemon-to-show', this.pokemonDetails);
      },
      sendPokemonToCurrentParty() {
        this.$emit('pokemon-to-add', this.pokemonDetails);
      },
    },
    props: ['pokemonurl'],
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
