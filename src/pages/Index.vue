<template>
  <Layout>
    <v-text-field
      autofocus
      :elevation="24"
      v-model="searchText"
      @click:clear="searchText = ''"
      placeholder="Search"
      style="max-width: 320px"
      class="mx-auto"
      prepend-inner-icon="mdi-magnify"
      color="white"
      clearable
      dense
      solo
      hide-details
    />
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

        <v-card-subtitle class="pb-0">{{ edge.node.long }}</v-card-subtitle>

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
  </Layout>
</template>

<page-query>
query {
  acronyms: allAcronym {
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
          return edge.node.short.toLowerCase().includes(x);
        } else if (edge.node.long.toLowerCase().includes(x)) {
          return edge.node.long.toLowerCase().includes(x);
        }
      });
    }
  }
};
</script>
