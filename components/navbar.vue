<template>
  <v-container>
    <v-toolbar height="60" elevation="2" rounded>
      <v-toolbar-title  >
        <h3 nuxt to="/" class="text-center">News Updates</h3>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn class="primary" nuxt to="/search-for-news">
        <span class="d-none d-sm-block"> search for news</span>
        <v-icon size="20">mdi-magnify</v-icon>
      </v-btn>
    </v-toolbar>
  </v-container>
</template>


<style>

</style>
