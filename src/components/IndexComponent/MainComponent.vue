<template>
  <main class="main bd-grid">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
    <!-- Search part-->

    <Search />
    <Movies />
    <informativ />
    <Character />
  </main>
</template>


<script>
import Search from "../SearchComponent/SearchComponent.vue";
import informativ from "../IndexComponent/InformativImageComponent.vue";
import Movies from "../MoviesComponent/MoviesListComponent.vue";
import Character from "../CharacterComponent/CharacterListComponent.vue";
export default {
  name: "MainComponent",
  components: {
    Search,
    informativ,
    Movies,
    Character,
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