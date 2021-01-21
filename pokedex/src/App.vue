<template>
  <h1>Welcome to the GEN 1 POKEDEX !!!</h1>
  <div v-if="loading">
    <p>LOADING, PLEASE WAIT</p>
  </div>
  <div v-else id="pokedex" class="container">
    <div class="row">
      <PartyManager v-bind:pokemontoadd="pokemonToAdd"></PartyManager>
      </div>
    <div class="row">
      <div class="col-4">
        <h3>The Pokédex</h3>
        <div class="pokemon" v-for="pokemon in pokedex" :key="pokemon.name">
          <Pokemon @pokemon-to-show="showPokemonInViewer" @pokemon-to-add="addPokemonToParty" v-bind:pokemonurl="pokemon.url"></Pokemon>
        </div>
      </div>
      <div class="viewer col-8">
        <PokeViewer v-bind:pokemonname="selectedPokemonName"></PokeViewer>
      </div>
    </div>
  </div>
</template>

<script>
  import Pokemon from './components/Pokemon.vue';
  import PokeViewer from './components/PokeViewer.vue';
  import PartyManager from "@/components/PartyManager";
  import axios from 'axios';

  export default {
    name: 'App',
    components: {
      Pokemon,
      PokeViewer,
      PartyManager
    },
    data() {
      return {
        // Get all gen 1 pokémons
        pokedex: axios.get('https://pokeapi.co/api/v2/pokemon?limit=151').then(response => {this.pokedex = response.data.results; this.loading = false;}),
        loading: true,
        selectedPokemonName: null,
        pokemonToAdd: null
      }
    },
    methods: {
      showPokemonInViewer(pokemon){
        this.selectedPokemonName = pokemon.name;
      },
      addPokemonToParty(pokemon) {
        if (this.pokemonToAdd === pokemon.name) {
          this.pokemonToAdd = null;
        }
        else {
          this.pokemonToAdd = pokemon.name;
        }
      }
    },
  }
</script>

<style>

</style>
