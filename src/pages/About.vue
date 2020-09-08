<template>
  <Layout>
    <v-container fluid>
      <v-row>
        <v-col sm="10" offset-sm="1">
          <v-card :elevation="20">
            <v-card-title class="text-h3">
              Masternym.
            </v-card-title>
            <v-card-subtitle class="text-overline font-weight-light">
              Mastercard's acronym dictionary.
            </v-card-subtitle>
            <v-divider></v-divider>
            <v-card-text>
              <div class="text-caption">
                Questions?
              </div>
              <div class="text-overline">
                Contact
                <span class="orange--text">tony@masternym.com</span>.
              </div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: "Info"
  }
};
</script>
