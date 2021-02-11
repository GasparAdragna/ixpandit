<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            PokeFinder
          </v-list-item-title>
          <v-list-item-subtitle>
            Made by:
            <a
              href="https://www.linkedin.com/in/gaspar-adragna-282945142/"
              target="_blank"
              >Gaspar Adragna</a
            >
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar class="black white--text" app>
      <v-app-bar-nav-icon
        @click="drawer = !drawer"
        color="white"
      ></v-app-bar-nav-icon>

      <v-toolbar-title>Gaspar's Pokemon Finder</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      items: [
        { title: "Home", icon: "mdi-view-dashboard", to: "/" },
        { title: "About", icon: "mdi-help-box", to: "/about" }
      ]
    };
  }
};
</script>
