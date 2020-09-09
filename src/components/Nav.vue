<template>
  <v-app-bar dark :elevation="20" class="flex-grow-0">
    <g-link to="/" class="text-decoration-none white--text">
      <div class="d-flex">
        <g-image src="~/assets/mc_symbol.svg" width="50" class="mr-3" />
        <v-toolbar-title class="text-overline">Masternym</v-toolbar-title>
      </div>
    </g-link>
    <v-spacer></v-spacer>
    <v-dialog v-model="dialog" persistent max-width="290">
      <template v-slot:activator="{ on, attrs }">
        <v-btn v-bind="attrs" v-on="on">About</v-btn>
      </template>
      <v-card>
        <v-card-title class="headline">About us</v-card-title>
        <v-card-text>
          <p>
            Masternym is a an acronym database that is super-fast, flexible
            and scalable.
          </p>
          <p>
            Have any questions, thoughts or feedback?
            <a class="yellow--text">Get in touch with us</a>
          </p>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="amber darken-1" text @click="dialog = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app-bar>
</template>

<script>
export default {
  name: "Nav",
  data() {
    return {
      dialog: false,
    };
  },
};
</script>