<template>
  <v-app class="overflow-hidden">
    <v-app-bar app dark :elevation="2">
      <g-link to="/">
        <g-image src="~/assets/logo.png" width="140" class="mt-1" />
      </g-link>
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
        solo
        hide-details
      />
      <g-link to="/about">
        <v-btn text small>About</v-btn>
      </g-link>
    </v-app-bar>
    <v-main>
      <v-container>
        <v-row>
          <v-col sm="10" offset-sm="1">
            <slot :searchText="searchText" />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<static-query>
query {
  metadata {
    siteName,
    siteDescription
  }
}
</static-query>

<script>
export default {
  data() {
    return {
      searchText: ""
    };
  }
};
</script>

<style scoped>
.v-app-bar a {
  text-decoration: none;
}
</style>
