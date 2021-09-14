<template>
  <div id="app">
    <Index />
    <Footer/>
  </div>
</template>

<script>
import Index from "./components/IndexComponent/IndexComponent.vue";
import Footer from "./components/FooterComponent/FooterComponent.vue"
export default {
  name: "app",
  components: {
    Index,
    Footer
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
