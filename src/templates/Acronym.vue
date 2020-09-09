<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="8" offset-sm="2">
          <v-card :elevation="2">
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
