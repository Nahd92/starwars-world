<template>
  <div class="show-more bd-grid">
    <div class="show-more-container">
      <div class="div-show">
        <a class="show-more-a-tag" @click="$emit('showMore')">SHOW MORE</a>
      </div>
      <div class="div-showNot">
        <a class="show-notMore-a-tag" @click="$emit('showNotMore')">Collapse</a>
      </div>
    </div>
  </div>
</template>

<!--CHILD-->
<script>
export default {
  name: "ShowMoreComponent",
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";
.show-more-container {
  width: 100%;
  background-color: var(--dark-color);
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: solid grey;
  opacity: 0.7;

  .show-more-a-tag,
  .show-notMore-a-tag {
    margin: 0.3em;
    text-align: center;
    font-size: 2em;
    color: grey;
    opacity: 0.8;

    &:hover {
      opacity: 1;
      transform: scale(1.03);
      color: white;
      text-decoration: underline;
      text-underline-position: under;
    }
  }
}
</style>