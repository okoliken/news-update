<template>
  <v-container>
    <span v-if="article != []" >
  <slot></slot>
    <v-card
      class="mx-auto my-3"
      max-width="600"
      v-for="(content, index) in article"
      :key="index"
      elevation="3"
    >
      <v-list-item three-line>
        <v-list-item-content>
          <div class="text-overline mb-4">
            {{ content.source.name }}
          </div>
          <h1 class="text-h5 mb-1">
            {{ content.title }}
          </h1>
          <v-list-item-subtitle>{{ content.content }}</v-list-item-subtitle>
          <v-img
            :src="content.urlToImage"
            :lazy-src="content.urlToImage"
            max-width="500"
            max-height="300"
          >
            <template v-slot:placeholder>
              <v-row class="fill-height ma-0" align="center" justify="center">
                <v-progress-circular
                  indeterminate
                  color="grey lighten-5"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-list-item-content>
      </v-list-item>

      <v-card-actions>
        <v-btn color="primary" rounded :href="content.url"> Learn More </v-btn>
      </v-card-actions>
    </v-card>
  </span>
  </v-container>
</template>

<script>
export default {
  props: {
    article: Array,
  },
};
</script>

<style></style>
