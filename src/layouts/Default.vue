<template>
  <v-app>
    <Nav />
    <v-main>
      <slot />
    </v-main>
    <v-footer color="primary lighten-1" padless>
      <v-row justify="center" no-gutters>
        <v-col
          class="grey darken-4 py-4 text-center white--text text-caption font-weight-light"
          cols="12"
        >
          {{ new Date().getFullYear() }} —
          Masternym by Digital Studio team
        </v-col>
      </v-row>
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

<script>
import Nav from "~/components/Nav.vue";

export default {
  components: {
    Nav,
  },
};
</script>

<style scoped>
.v-app-bar a {
  text-decoration: none;
}
</style>
