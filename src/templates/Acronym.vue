<template>
  <Layout>
    <v-card :elevation="20">
      <v-card-title class="text-h3">
        {{ $page.acronym.short }}
      </v-card-title>
      <v-card-subtitle class="text-overline">
        {{ $page.acronym.long }}
      </v-card-subtitle>
      <v-divider></v-divider>
      <v-card-text>
        <div class="text-caption">Example</div>
        <div class="text-overline">{{ $page.acronym.example }}</div>
      </v-card-text>
    </v-card>
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
  metainfo() {
    return {
      title: this.$page.acronym.short
    };
  }
};
</script>
