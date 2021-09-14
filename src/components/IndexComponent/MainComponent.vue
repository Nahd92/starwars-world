<template>
  <main class="main bd-grid">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
    <!-- Search part-->
    <Search />
    <Movies />
  </main>
</template>

<script>
import Search from "../SearchComponent/SearchComponent.vue";

import Movies from "../MoviesComponent/MoviesListComponent.vue";
export default {
  name: "MainComponent",
  components: {
    Search,
    Movies,
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.main {
  background-color: var(--dark-color);
  width: 100%;
}
</style>