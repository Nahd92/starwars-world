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
import Header from "./HeaderComponent.vue";
import Welcome from "./WelcomeComponent.vue";
import Footer from "../FooterComponent/FooterComponent.vue";
import Main from "./MainComponent.vue";

export default {
  name: "IndexComponent",
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