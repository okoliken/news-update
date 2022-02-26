<template>
  <v-app dark>
  <navbar/>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import navbar from '~/components/navbar.vue';
export default {
  components: { navbar },
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Headlines",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Headlines",
          to: "/inspire",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Daily news",
    };
  },
};
</script>
