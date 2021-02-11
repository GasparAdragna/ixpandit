<template>
  <div class="home">
    <v-row v-if="!ready">
      <v-col cols="12" justify="center" class="text-center">
        <v-progress-circular
          :size="50"
          color="primary"
          indeterminate
          class="text-center"
        ></v-progress-circular>
        <h2>Loading pokemons...</h2>
      </v-col>
    </v-row>
    <v-row v-else>
      <v-col
        cols="12"
        v-for="(pokemon, index) in pokemons.results"
        :key="index"
      >
        {{ pokemon.name }}
      </v-col>
    </v-row>
  </div>
</template>

<script>
var Pokedex = require("pokedex-promise-v2");
var P = new Pokedex();
const Swal = require("sweetalert2");
export default {
  name: "Home",
  data() {
    return {
      pokemons: {},
      ready: false
    };
  },
  created: async function() {
    this.ready = false;
    if (localStorage.pokemons) {
      P.getPokemonsList() // with Promise
        .then(function(response) {
          localStorage.setItem("pokemons", JSON.stringify(response));
        })
        .catch(function() {
          Swal.fire({
            icon: "error",
            title: "Oops...",
            text: "Something went wrong while trying to fetch the pokemons!"
          });
        });
    }
    let retrievedObject = localStorage.getItem("pokemons");
    this.pokemons = JSON.parse(retrievedObject);
    this.ready = true;
  }
};
</script>
