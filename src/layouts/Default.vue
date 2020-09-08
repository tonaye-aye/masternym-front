<template>
  <v-app class="overflow-hidden">
    <v-app-bar app dark :elevation="6">
      <g-link to="/">
        <g-image src="~/assets/logo.png" width="140" class="mt-1" />
      </g-link>
      <v-spacer />
      <g-link to="/about">
        <v-btn text small>About</v-btn>
      </g-link>
    </v-app-bar>
    <v-main>
      <v-container>
        <v-row>
          <v-col sm="10" offset-sm="1">
            <slot />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
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
