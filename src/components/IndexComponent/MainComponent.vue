<template>
  <main class="main bd-grid">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
    <!-- Search part-->
    <Search />
    <Movies />
  </main>
</template>

<Character/>
<script>

import Character from "../CharacterComponent/CharacterListComponent.vue"
export default {
  name: "MainComponent",
  componets:{
    Character

  }
  
  
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.main {
  background-color: var(--dark-color);
  width: 100%;
}
</style>