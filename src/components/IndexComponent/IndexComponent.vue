<template>
  <div class="startwars-project">
    <!-- Här ska alla delar som ska finnas i HELA Index  importeras in -->

    <Header />
    <!-- Welcome part-->
    <Welcome />

    <!-- Search part-->
    <Search />

    <!-- Main Part -->

    <!-- Footer Part -->
  </div>
</template>

<script>
import Header from "./HeaderComponent.vue";
import Welcome from "./WelcomeComponent.vue";
import Search from "../SearchComponent/SearchComponent.vue";

export default {
  name: "IndexComponent",
  components: {
    Header,
    Welcome,
    Search,
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";
</style>