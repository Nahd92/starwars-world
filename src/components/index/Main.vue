<template>
  <main class="main bd-grid">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
    <!-- Search part-->

    <Search />
    <Movies />
    <Informativ />
    <Character />
  </main>
</template>


<script>
import Search from "../search/Search.vue";
import Informativ from "./InformativImage.vue";
import Movies from "../movies/Movies.vue";
import Character from "../character/Characters.vue";
export default {
  name: "Main",
  components: {
    Search,
    Informativ,
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