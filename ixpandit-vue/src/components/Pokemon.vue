<template>
  <v-card class="mx-auto">
    <v-card-text>
      <p class="display-1 text--primary mb-0">
        {{ capitalizedName }}
      </p>
    </v-card-text>
    <v-card-actions>
      <v-btn text color="deep-purple accent-4">
        Learn More
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "Pokemon",
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
  }
};
</script>

<style lang="css" scoped></style>
