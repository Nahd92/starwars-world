<template>
  <div id="app">
    <Index />
  </div>
</template>

<script>
import Index from "./components/IndexComponent/IndexComponent.vue";
export default {
  name: "app",
  components: {
    Index,
  },
};
</script>

<style lang="scss">
@import "./style/styles.scss";
</style>
