<template>
  <v-app>
    <Header></Header>
    <HomePage></HomePage>
    <Footer></Footer>
  </v-app>
</template>

<script>
//Import components for register
import Header from "./views/Header.vue";
import HomePage from "./components/HomePage.vue";
import Footer from "./views/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    HomePage,
    Footer,
  },
  data: () => ({
    //
  }),
};
</script>
