<template>
  <section>
    <h2 class="card-title characters-title">All Character</h2>
    <div :style="{ height: containerHeight + 'em' }" class="card-container">
      <div
        class="card"
        v-for="(character, index) in characters"
        v-bind:key="character.id"
      >
        <div class="card-img">
          <img :src="character.characterCover" alt="luke" />
        </div>
        <div class="card-information">
          <h3 class="card-name">{{ character.name }}</h3>
        </div>
        <div class="card-button">
          <CharacterModal :character="characters[index]" :movies="movies" />
        </div>
      </div>
    </div>

    <div class="show-more-cont characters-more-cont">
      <!--PARENT-->
      <ShowMore
        v-on:showMore="increaseHeight()"
        v-on:showNotMore="setHeightToDefault()"
      />
    </div>
  </section>
</template>
<script>
import CharacterModal from "../modal/CharacterModal.vue";
import ShowMore from "../showMore/ShowMore.vue";
export default {
  components: {
    ShowMore,
    CharacterModal,
  },
  props: {
    characters: {
      type: Array,
      default: () => [],
    },
    movies: {
      type: Array,
      default: () => [],
    },
  },
  name: "Characters",
  data: () => ({
    fetchCharacters: [],
    pages: 1,
    containerHeight: 60,
    containerMaxHeight: false,
  }),

  methods: {
    increaseHeight() {
      if (this.containerHeight >= 500) {
        this.containerHeight = 500;
      } else this.containerHeight += 55;
    },
    setHeightToDefault() {
      this.containerHeight = 60;
    },
    containerHeightMax() {
      if (this.containerHeight >= 800) {
        this.containerHeight = !this.containerHeight;
      }
    },
  },
};
</script>
<style lang="scss" scoped>
@import "./style/styles.scss";

h3,
p {
  color: black;
}

.characters-title {
  margin-top: 1em;
}
.characters-more-cont {
  margin-bottom: 0;
}

.card-container {
  .card {
    width: 14em;
  }
}
</style>