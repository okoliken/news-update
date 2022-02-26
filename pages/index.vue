<template>
  <v-container>
    <back-to-top/>

    <v-row justify="space-between">
      <v-col cols="12" sm="6" md="6">
        <v-sheet class="pa-3 mb-4" v-if="isFetching === true">
          <v-skeleton-loader
            class="mx-auto mb-5"
            v-for="i in 5"
            :key="i"
            type="card"
          ></v-skeleton-loader>
        </v-sheet>
        <news-article v-else :article="newsArticlesFromUs">
          <h1>Top Headlines</h1>
        </news-article>
      </v-col>
      <v-col cols="12" sm="6" md="6">
        <v-sheet class="pa-3 mb-4" v-if="isFetching === true">
          <v-skeleton-loader
            class="mx-auto mb-5"
            v-for="i in 5"
            :key="i"
            type="card"
          ></v-skeleton-loader>
        </v-sheet>

        <news-article v-else :article="newsArticlesFromUk">
          <h1>Headlines From UK</h1>
        </news-article>
      </v-col>
    </v-row>
    <v-row justify="space-between my-2">
      <v-col cols="12" sm="6" md="6">
        <v-sheet class="pa-3 mb-4" v-if="isFetching === true">
          <v-skeleton-loader
            class="mx-auto mb-5"
            v-for="i in 5"
            :key="i"
            type="card"
          ></v-skeleton-loader>
        </v-sheet>
        <news-article v-else :article="newsArticleFromTec">
          <h1>Top headlines from TechCrunch right now</h1>
        </news-article>
      </v-col>

      <v-col cols="12" sm="6" md="6">
        <v-sheet class="pa-3 mb-4" v-if="isFetching === true">
          <v-skeleton-loader
            class="mx-auto mb-5"
            v-for="i in 5"
            :key="i"
            type="card"
          ></v-skeleton-loader>
        </v-sheet>

        <news-article v-else :article="nigerianNews">
          <h1>Headlines From Nigeria</h1>
        </news-article>
      </v-col>
    </v-row>
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
        <news-article v-else :article="southAfrica">
          <h1>Top headlines from South Africa</h1>
        </news-article>
      </v-col>
    </v-row>


  </v-container>
</template>

<script>
import newsArticle from "~/components/news-article.vue";
import backToTop from "~/components/back-to-top.vue"
import axios from "@nuxtjs/axios";
export default {
  components: { newsArticle, backToTop },
  name: "IndexPage",
  data() {
    return {
      apiKey: {
        US: "4741e04af28c4e43bc910fdea65c32ce",
        nigeria: "ba1156818eda46acbf80a61b8fe90e59",
      },
      isFetching: false,
      newsArticlesFromUs: [],
      newsArticlesFromUk: [],
      newsArticleFromTec: [],
      nigerianNews: [],
      southAfrica: [],
    };
  },
  methods: {
    async getHeadlinesFromUs() {
      console.log("ggg ");
      try {
        //
        this.isFetching = true;
        const req = await this.$axios.$get(
          `https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=${this.apiKey.US}`
        );
        const data = await req;
        this.isFetching = false;
        this.newsArticlesFromUs = data.articles;
      } catch (error) {
        console.log(error);
      }
    },

    async getHeadlinesFromUk() {
      try {
        this.isSearching = true;
        const req = await this.$axios.$get(
          `https://newsapi.org/v2/top-headlines?country=gb&apiKey=${this.apiKey.nigeria}`
        );
        const data = await req;
        this.isFetching = false;
        this.newsArticlesFromUk = data.articles;
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    },
    async getTechcrunchNews() {
      try {
        this.isSearching = true;
        const req = await this.$axios.$get(
          `https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=${this.apiKey.nigeria}`
        );
        const data = await req;
        this.isFetching = false;
        this.newsArticleFromTec = data.articles;
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    },
    async getNigeriaNews() {
      try {
        this.isSearching = true;
        const req = await this.$axios.$get(
          `https://newsapi.org/v2/top-headlines?country=ng&apiKey=${this.apiKey.nigeria}`
        );
        const data = await req;
        this.isFetching = false;
        this.nigerianNews = data.articles;
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    },
    async getSouthAfricaNews() {
      try {
        this.isSearching = true;
        const req = await this.$axios.$get(
          `https://newsapi.org/v2/top-headlines?country=za&category=entertainment&apiKey=${this.apiKey.nigeria}`
        );
        const data = await req;
        this.isFetching = false;
        this.southAfrica = data.articles;
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    this.getHeadlinesFromUs();
    this.getHeadlinesFromUk();
    this.getTechcrunchNews();
    this.getNigeriaNews();
    this.getSouthAfricaNews();
  },
};
</script>

<style scoped>




</style>
