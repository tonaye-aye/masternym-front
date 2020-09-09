<template>
  <v-app>
    <v-app-bar dark :elevation="20" class="flex-grow-0">
      <g-link to="/">
        <g-image src="~/assets/mc_symbol.svg" width="50" />
      </g-link>
      <v-spacer></v-spacer>
      <v-dialog v-model="dialog" persistent max-width="290">
        <template v-slot:activator="{ on, attrs }">
          <v-btn v-bind="attrs" v-on="on">About</v-btn>
        </template>
        <v-card>
          <v-card-title class="headline">About us</v-card-title>
          <v-card-text>
            <p>
              Masternym is a an acronym database that is super-fast, flexible
              and scalable.
            </p>
            <p>
              Have any questions, thoughts or feedback?
              <a class="amber--text">Get in touch with us</a>
            </p>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="orange darken-1" text @click="dialog = false">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-app-bar>
    <v-main>
      <slot />
    </v-main>
    <v-footer
      class="text-center d-block pt-4 pb-6 text-overline font-weight-light black"
    >2020 — Managed Services</v-footer>
  </v-app>
</template>

<static-query>
query {
  metadata {
    siteName,
    siteDescription
  }
}
</static-query>

<script>
export default {
  data() {
    return {
      dialog: false,
    };
  },
};
</script>

<style scoped>
.v-app-bar a {
  text-decoration: none;
}
</style>
