<template>
  <v-footer color="primary lighten-1" padless>
    <v-row justify="center" no-gutters>
      <v-col class="grey darken-4 py-4 text-center white--text text-overline" cols="12">
        {{ new Date().getFullYear() }} —
        Masternym by Digital Studio team
      </v-col>
    </v-row>
  </v-footer>
</template>

<script>
export default {
  name: "Nav",
};
</script>