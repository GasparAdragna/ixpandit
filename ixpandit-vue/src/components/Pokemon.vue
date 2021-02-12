<template>
  <div class="">
    <v-card class="mx-auto">
      <v-card-text>
        <p class="display-1 text--primary mb-0">
          {{ capitalizedName }}
        </p>
      </v-card-text>
      <v-card-actions>
        <v-dialog v-model="dialog" width="500" content-class="elevation-0">
          <!-- <template v-slot:activator="{ on, attrs }">
            <v-btn color="red lighten-2" dark v-bind="attrs" v-on="on">
              Click Me
            </v-btn>
          </template> -->
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="deep-purple accent-4"
              text
              v-bind="attrs"
              v-on="on"
              @click="showInfo()"
            >
              Learn More
            </v-btn>
          </template>

          <v-card
            class="mx-auto my-12"
            max-width="500"
            v-if="pokemonDetails.hasOwnProperty('sprites')"
          >
            <v-img :src="pokemonDetails.sprites.front_default"></v-img>

            <v-card-title class="text-h2">{{ capitalizedName }}</v-card-title>

            <v-divider class="mx-4"></v-divider>
            <!-- Tipo de Pokemon -->
            <v-card-title>Pokemon Type</v-card-title>
            <v-card-text class="pb-0">
              <v-chip-group
                active-class="deep-purple accent-4 white--text"
                column
              >
                <v-chip
                  v-for="(type, index) in pokemonDetails.types"
                  :key="index"
                  >{{ type.type.name }}</v-chip
                >
              </v-chip-group>
            </v-card-text>
            <!-- Movimientos -->
            <v-card-title>Moves</v-card-title>
            <v-card-text>
              <v-chip-group
                active-class="deep-purple accent-4 white--text"
                column
              >
                <v-chip
                  v-for="(move, index) in pokemonDetails.moves"
                  :key="index"
                  >{{ move.move.name }}</v-chip
                >
              </v-chip-group>
            </v-card-text>
          </v-card>
        </v-dialog>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
// var Pokedex = require("pokedex-promise-v2");
// var P = new Pokedex();
const Swal = require("sweetalert2");
const axios = require("axios");

export default {
  name: "Pokemon",
  data() {
    return {
      dialog: false,
      pokemonDetails: {}
    };
  },
  props: {
    name: {
      type: String,
      required: true
    }
  },
  computed: {
    capitalizedName() {
      return this.name.charAt(0).toUpperCase() + this.name.slice(1);
    }
  },
  methods: {
    async showInfo() {
      try {
        const response = await axios.get(
          "https://pokeapi.co/api/v2/pokemon/" + this.name
        );
        this.pokemonDetails = response.data;
      } catch (e) {
        Swal.fire({
          icon: "error",
          title: "Oops...",
          text: "Something went wrong while trying learn more from Pokemon",
          footer: "Please refresh the page and try again"
        });
      }
    }
  }
};
</script>

<style lang="css" scoped></style>
