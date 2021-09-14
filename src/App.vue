<template>
  <div id="app">
    <Index />
    <movies-list-component />
  </div>
</template>

<script>
import Index from "./components/IndexComponent/IndexComponent.vue";
import MoviesListComponent from "./components/MoviesComponent/MoviesListComponent.vue";
export default {
  name: "app",
  components: {
    Index,
    MoviesListComponent,
  },
};
</script>

<style lang="scss">
@import "./style/styles.scss";

body {
  background: url(./assets/welcome-stars.jpg) repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
}
</style>
