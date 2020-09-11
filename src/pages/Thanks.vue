<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <p class="text-h5 font-weight-light mb-5">Thanks for getting in touch!</p>
          <v-btn @click="$router.push(`/`)">Home</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: "Thanks!",
  },
};
</script>
