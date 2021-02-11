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
      <v-col cols="12" class="mt-5">
        <h1>Search your favourite Pokemon...</h1>
        <v-text-field v-model="searchInput" placeholder="Enter Pokemon Name..."
          >Search por pokemon...</v-text-field
        >
      </v-col>
      <v-row>
        <v-col
          cols="12"
          lg="3"
          v-for="(pokemon, index) in filteredPokemons"
          :key="index"
        >
          <Pokemon :name="pokemon.name"></Pokemon>
        </v-col>
      </v-row>
      <v-btn class="mt-5" color="primary" @click="morePokemons()" block>
        Load more Pokemons
      </v-btn>
    </v-row>
  </div>
</template>

<script>
var Pokedex = require("pokedex-promise-v2");
var P = new Pokedex();
const Swal = require("sweetalert2");
import Pokemon from "../components/Pokemon.vue";
export default {
  name: "Home",
  components: { Pokemon },
  data() {
    return {
      pokemons: {},
      searchInput: null,
      ready: false,
      limit: 10
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
  },
  computed: {
    filteredPokemons: function() {
      let result = this.pokemons.results;
      if (this.searchInput != null) {
        result = this.pokemons.results.filter(
          item =>
            item.name.toUpperCase().indexOf(this.searchInput.toUpperCase()) > -1
        );
      }
      return result.slice(0, this.limit);
    }
  },
  methods: {
    morePokemons() {
      this.limit += 10;
    }
  }
};
</script>
