<template>
  <Layout>
    <v-banner app dark color="amber accent-4">
      <p
        class="text-center text-md-h5 font-weight-light black--text text--lighten-3"
      >
        Mastercard acronyms, all in one place.
      </p>
      <v-text-field
        autofocus
        :elevation="24"
        v-model="searchText"
        @click:clear="searchText = ''"
        placeholder="Search"
        style="max-width: 320px;"
        class="mx-auto"
        prepend-inner-icon="mdi-magnify"
        color="white"
        clearable
        solo
        hide-details
      />
    </v-banner>
    <v-container fluid>
      <v-row>
        <v-col sm="10" offset-sm="1">
          <v-row class="justify-center align-center">
            <v-card
              :elevation="24"
              v-for="edge in searchEvents(searchText)"
              :key="edge.node.short"
              max-width="280px"
              width="100%"
              class="mt-6 ml-2 mr-2 align-self-stretch align-center"
            >
              <v-card-title>{{ edge.node.short }}</v-card-title>

              <v-card-subtitle class="pb-0">{{
                edge.node.long
              }}</v-card-subtitle>

              <v-card-actions>
                <v-btn
                  @click="$router.push(`/acronyms/${edge.node.short}`)"
                  color="orange"
                  text
                  >Details</v-btn
                >
              </v-card-actions>
            </v-card>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<page-query>
query {
  acronyms: allAcronym(sortBy: "short", order: ASC) {
    edges {
      node {
        id
        short
        long
        example
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: "Masternym"
  },
  data() {
    return {
      acronyms: [],
      searchText: ""
    };
  },
  mounted() {
    this.acronyms = this.$page.acronyms.edges;
  },
  methods: {
    searchEvents(searchText) {
      let x = searchText.toLowerCase();
      return this.acronyms.filter((edge) => {
        if (edge.node.short.toLowerCase().includes(x)) {
          let match = edge.node.short.toLowerCase().includes(x);
          return match;
        } else if (edge.node.long.toLowerCase().includes(x)) {
          let match = edge.node.long.toLowerCase().includes(x);
          return match;
        }
      });
    }
  }
};
</script>
