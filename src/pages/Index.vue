<template>
  <Layout>
    <v-banner app dark class="orange accent-2">
      <v-text-field
        autofocus
        :elevation="2"
        v-model="searchText"
        @click:clear="searchText = ''"
        placeholder="Search acronyms fast..."
        style="max-width: 320px;"
        class="mx-auto"
        prepend-inner-icon="mdi-magnify"
        color="white"
        clearable
        solo
        hide-details
      />
    </v-banner>
    <v-container>
      <v-row class="justify-center align-center">
        <v-card
          :elevation="2"
          v-for="edge in searchEvents(searchText)"
          :key="edge.node.short"
          max-width="320px"
          width="100%"
          class="mt-4 mx-2 align-self-stretch align-center"
        >
          <v-card-title>{{ edge.node.short }}</v-card-title>

          <v-card-subtitle class="pb-1">{{ edge.node.long }}</v-card-subtitle>

          <v-card-actions>
            <v-btn @click="$router.push(`/acronyms/${edge.node.short}`)" color="orange" text>Learn</v-btn>
          </v-card-actions>
        </v-card>
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
    title: "Acronyms",
  },
  data() {
    return {
      acronyms: [],
      searchText: "",
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
          return edge.node.short.toLowerCase().includes(x);
        } else if (edge.node.long.toLowerCase().includes(x)) {
          return edge.node.long.toLowerCase().includes(x);
        }
      });
    },
  },
};
</script>
