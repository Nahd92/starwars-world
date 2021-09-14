<template>
  <main class="main">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
  </main>
</template>

<script>
export default {
  name: "MainComponent",
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.main {
  background-color: var(--dark-color);
  height: 100vh;
  width: 100%;
}
</style>