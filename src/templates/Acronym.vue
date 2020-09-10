<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <v-card>
            <v-card-title class="text-h3">{{ $page.acronym.short }}</v-card-title>
            <v-card-subtitle class="text-subtitle-1 font-weight-light">{{ $page.acronym.long }}</v-card-subtitle>
            <v-card-text>
              <blockquote class="blockquote">
                <span class="text-body-2 font-italic">Example:</span>
                <br />
                <span class="text-caption">{{ $page.acronym.example }}</span>
              </blockquote>
            </v-card-text>
            <v-card-actions>
              <v-btn text color="amber darken-1" @click="$router.push(`/`)">Back</v-btn>
              <v-spacer></v-spacer>
              <v-btn icon>
                <v-icon>mdi-heart</v-icon>
              </v-btn>
              <v-btn icon>
                <v-icon>mdi-share-variant</v-icon>
              </v-btn>
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
      title: this.$page.acronym.short,
    };
  },
};
</script>
