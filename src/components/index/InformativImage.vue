<template>
  <section class="informativ-section">
    <div class="informativ-container">
      <div class="info-img">
        <img src="../../assets/movies/a-new-hope.jpg" alt="galaxy" />
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "InformativImage",
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.informativ-section {
  height: 25em;
  overflow: hidden;
  .informativ-container {
    position: absolute;
    top: -4.8em;
    overflow: hidden;
    width: 100%;
    position: relative;
    img {
      height: 40em;
      width: 100%;
    }
  }
  -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
    5px 5px 15px 5px rgba(0, 0, 0, 0);
  box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
    5px 5px 15px 5px rgba(0, 0, 0, 0);
}
@media screen and (max-width: 590px) {
  .informativ-section {
    height: 15em;

    .informativ-container {
      top: 0em;

      img {
        height: 20em;
        width: 100%;
      }
    }
  }
}
</style>