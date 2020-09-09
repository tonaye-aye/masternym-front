<template>
  <v-app>
    <Nav />
    <v-main>
      <slot />
    </v-main>
    <!-- <v-footer
      class="text-center d-block pt-4 pb-6 text-overline font-weight-light black"
    >2020 — Mastercard, Sydney</v-footer>-->
    <Footer />
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
import Footer from "~/components/Footer.vue";

export default {
  components: {
    Nav,
    Footer,
  },
};
</script>

<style scoped>
.v-app-bar a {
  text-decoration: none;
}
</style>
