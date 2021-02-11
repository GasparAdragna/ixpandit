<template>
  <div class="home">
    <v-row>
      <v-col> </v-col>
    </v-row>
  </div>
</template>

<script>
var Pokedex = require("pokedex-promise-v2");
var P = new Pokedex();
export default {
  name: "Home",
  data() {
    return {
      pokemons: {}
    };
  },
  created: async function() {
    P.getPokemonByName("eevee") // with Promise
      .then(function(response) {
        console.log(response);
      })
      .catch(function(error) {
        console.log("There was an ERROR: ", error);
      });
  }
};
</script>
