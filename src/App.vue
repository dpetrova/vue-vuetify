<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title>Vuetify Dashboard</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn 
        v-for="link in links"
        :key="`${link.label}-header-link`"
        text
        rounded
        :to="link.url"
      >
      {{link.label}}
      </v-btn>
      <!-- to toggle light/dark theme -->
      <v-btn @click="toggleTheme" text rounded>
        Toggle Theme
      </v-btn>     
    </v-app-bar>
    <v-main>
      <router-view></router-view>
    </v-main>
    <v-footer color="primary lighten-1" padless>
      <v-layout justify-center wrap>
        <v-btn
          v-for="link in links"
          :key="`${link.label}-footer-link`"
          color="white"
          text
          rounded
          :to="link.url"
          class="my-2"
        >
          {{ link.label }}
        </v-btn>
        <v-flex primary lighten-2 py-4 text-center white--text xs12>
          {{ new Date().getFullYear() }} — <strong>Vuetify Dashboard</strong>
        </v-flex>
      </v-layout>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    links: [
      {
        label: "Home",
        url: "/"
      },
      {
        label: "Login",
        url: "/login"
      },
      {
        label: "Signup",
        url: "/signup"
      },
      {
        label: "Dashboard",
        url: "/dashboard"
      }
    ]
  }),
  methods: {
    toggleTheme() {
      //change anchor color in dark theme
      this.$vuetify.theme.themes.dark.anchor = "#41B883";
      //toggle between light/dark theme
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    }
  }
};
</script>
