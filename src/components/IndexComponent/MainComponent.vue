<template>
  <main class="main bd-grid">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
    <!-- Search part-->
    <Search />
    <Movies />
  </main>
</template>

<Char
<script>
<<<<<<< HEAD

import Character from "../CharacterComponent/CharacterListComponent.vue"
export default {
  name: "MainComponent",
  data:()
=======
import Search from "../SearchComponent/SearchComponent.vue";

import Movies from "../MoviesComponent/MoviesListComponent.vue";
export default {
  name: "MainComponent",
  components: {
    Search,
    Movies,
  },
>>>>>>> 3f53fc36629b134550e9e60b7154d01b7d3fccc4
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.main {
  background-color: var(--dark-color);
  width: 100%;
}
</style>