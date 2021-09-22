<template>
  <div id="app">
    <Index />
  </div>
</template>

<script>
import Index from "./components/index/Index.vue";

export default {
  name: "app",
  components: {
    Index,
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
