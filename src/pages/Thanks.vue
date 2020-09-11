<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <p class="text-h5 font-weight-light grey--text mb-5">/Thanks</p>
          <v-card class="pa-4">
            <p class="text-overline font-weight-light">We have received your message</p>
            <v-btn color="orange black--text" @click="$router.push(`/`)">Home</v-btn>
          </v-card>
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



<v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <p class="text-h5 font-weight-light grey--text mb-5">/acronyms/{{ $page.acronym.short }}</p>

        </v-col>
      </v-row>
    </v-container>