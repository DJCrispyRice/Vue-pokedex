<template>
  <div id="app">
    <h1>Welcome to the GEN 1 POKEDEX !!</h1>
    <div id="pokedex" class="container">
      <div class="row">
        <div class="col-4">
          <div class="pokemon" v-for="pokemon in pokedex" :key="pokemon.name">
            <Pokemon @pokemon-to-show="showPokemonInViewer" v-bind:pokemonurl="pokemon.url"></Pokemon>
          </div>
        </div>
        <div class="viewer col-8">
          <PokeViewer v-bind:pokemonname="selectedPokemonName"></PokeViewer>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Pokemon from './components/Pokemon.vue';
  import PokeViewer from './components/PokeViewer.vue';
  import axios from 'axios';

  export default {
    name: 'App',
    components: {
      Pokemon,
      PokeViewer
    },
    data() {
      return {
        // Get all gen 1 pokémons
        pokedex: axios.get('https://pokeapi.co/api/v2/pokemon?limit=151').then(response => this.pokedex = response.data.results),
        selectedPokemonName: null
      }
    },
    methods: {
      showPokemonInViewer(pokemon){
        this.selectedPokemonName = pokemon.name;
      }
    },
  }
</script>

<style>

</style>
