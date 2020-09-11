<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <p class="text-h5 font-weight-light grey--text mb-5">
            /acronyms/{{ $page.acronym.short }}
          </p>
          <v-card>
            <v-card-title class="text-h3">{{
              $page.acronym.short
            }}</v-card-title>
            <v-card-subtitle class="text-overline font-weight-light">{{
              $page.acronym.long
            }}</v-card-subtitle>
            <v-card-text>
              <blockquote class="blockquote black--text orange accent-2">
                <div class="text-caption font-italic mb-1">Example:</div>
                <div class="text-body-1">{{ $page.acronym.example }}</div>
              </blockquote>
            </v-card-text>
            <v-card-actions>
              <v-btn text color="orange" @click="$router.push(`/`)">Back</v-btn>
              <v-spacer></v-spacer>
              <v-tooltip bottom>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn icon v-bind="attrs" v-on="on">
                    <v-icon>mdi-heart</v-icon>
                  </v-btn>
                </template>
                <span>'Favourite' coming soon</span>
              </v-tooltip>
              <v-tooltip bottom open-on-click>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn icon v-bind="attrs" v-on="on">
                    <v-icon>mdi-share-variant</v-icon>
                  </v-btn>
                </template>
                <span>'Share' coming soon</span>
              </v-tooltip>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
    acronym(id: $id) {
        id
        short
        long
        example
    }
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.acronym.short
    };
  }
};
</script>
