<template>
  <header class="header">
    <!-- Här ska alla delar som ska finnas i HEADER importeras in -->
    <Navbar />
  </header>
</template>

<script>
import Navbar from "../navbar/Navbar.vue";
export default {
  name: "Header",
  components: {
    Navbar,
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.header {
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: var(--z-fixed);
}
</style>