<template>
  <v-container>
    <v-btn nuxt to="/" color="primary pb-1"> go back </v-btn>
    <h1>Search for specific content</h1>
    <v-flex class="d-flex justify-center py-5">
      <v-text-field
        label="Outlined"
        placeholder="Placeholder"
        outlined
        v-model.lazy="query"
        dense
      ></v-text-field>
      <v-btn :loading="isFetching" @click="getNewsBySearch()" color="primary">
        <v-icon size="30">mdi-magnify</v-icon>
      </v-btn>
    </v-flex>
    <v-main>
      <v-btn
        v-if="searchResponse.length > 0"
        :loading="isFetching"
        @click="clearSearch()"
        color="primary"
      >
        clear search
      </v-btn>
      <p>Searched News would appear here</p>
      <back-to-top    v-if="searchResponse.length > 0"/>
      <v-container>
      <h1>{{query}}</h1>
        <v-row class="space-between my-2">
          <v-col cols="12" sm="6" md="6">
            <v-sheet class="pa-3 mb-4" v-if="isFetching === true">
              <v-skeleton-loader
                class="mx-auto mb-5"
                v-for="i in 5"
                :key="i"
                type="card"
              ></v-skeleton-loader>
            </v-sheet>
            <news-article v-else :article="searchResponse">
              <h1></h1>
            </news-article>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-container>
</template>

<script>
import axios from "@nuxtjs/axios";
import backTotop from "~/components/back-to-top.vue";
const date = new Date();

const fullDate =
  date.getFullYear() + "-" + date.getMonth() + "-" + date.getDate();

console.log(fullDate);

export default {
  data() {
    return {
      isFetching: false,
      query: "",
      US: "4741e04af28c4e43bc910fdea65c32ce",
      searchResponse: [],
    };
  },
  components: { backTotop },
  methods: {
    async getNewsBySearch() {
      this.isFetching = true;
      const req = await this.$axios.$get(
        `https://newsapi.org/v2/everything?q=${this.query}&from=${fullDate}&sortBy=popularity&apiKey=${this.US}`
      );
      const data = await req;
      console.log(data);
      this.searchResponse = data.articles;
      this.isFetching = false;
    },
    clearSearch() {
      this.searchResponse = "";
    },
  },
};
</script>

<style></style>
