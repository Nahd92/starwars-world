<template>
  <div class="startwars-project">
    <!-- Här ska alla delar som ska finnas i HELA Index  importeras in -->

    <Header />
    <!-- Welcome part-->
    <Welcome />

    <!-- Main Part -->
    <Main />

    <!-- Footer Part -->
    <Footer />
  </div>
</template>

<script>
import Header from "./Header.vue";
import Welcome from "./Welcome.vue";
import Footer from "../footer/Footer.vue";
import Main from "./Main.vue";

export default {
  name: "Index",
  components: {
    Header,
    Welcome,
    Main,
    Footer,
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";
</style>