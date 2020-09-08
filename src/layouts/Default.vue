<template>
  <v-app>
    <v-app-bar app dark :elevation="2">
      <g-link to="/">
        <g-image src="~/assets/logo.png" width="120" class="mt-1" />
      </g-link>
      <v-spacer></v-spacer>
      <g-link to="/about">
        <v-btn text small>About</v-btn>
      </g-link>
    </v-app-bar>
    <v-main>
      <slot :searchText="searchText" />
    </v-main>
    <v-footer
      class="text-center d-block pt-4 pb-6 text-overline font-weight-light black"
    >
      2020 — Managed Services
    </v-footer>
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

<style scoped>
.v-app-bar a {
  text-decoration: none;
}
</style>
