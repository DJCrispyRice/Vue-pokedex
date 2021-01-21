<template>
  <div class="partymanager">
    <h3>Your team - click a pokémon to delete it from your party</h3>
    <div v-if="currentTeam.length">
      <div class="row">
        <div class="team" v-for="pokemon in currentTeam" :key="pokemon.name">
        <span>
          <img class="mr-0" v-bind:src="pokemon.sprites.front_default"/>
        </span>
        </div>
      </div>
    </div>
    <div v-else>
      Your party is empty. You can add up to 6 pokemon in it !
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: "PartyManager",
    data() {
      return {
        currentTeam: []
      }
    },
    props: ['pokemontoadd'],
    watch: {
      pokemontoadd: function(newPokemonName) {
        if (this.currentTeam.length >= 6) {
          alert("Your party is full, you can't add "+newPokemonName);
        }
        else {
          if (this.currentTeam.find(pokemon => pokemon.name === newPokemonName) || !newPokemonName) {
            alert("This pokemon is already in your party !");
          }
          else {
            axios.get('https://pokeapi.co/api/v2/pokemon/'+newPokemonName).then(response => this.currentTeam.push(response.data));
          }
        }
      }
    },
  }
</script>

<style scoped>

</style>