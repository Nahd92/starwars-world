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
      <h3 class="char-length">
        Number of characters:
        {{ characters.length }}
      </h3>
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
    charactersLength: 10,
  }),
  methods: {
    increaseHeight() {
      this.containerHeight += 55;
      //this.reduceCharLengthOnClick();
    },
    //reduceCharLengthOnClick() {
    // if (this.charactersLength >= this.characters.length - 2) {
    //   this.charactersLength = this.characters.length;
    // } else {
    //   this.charactersLength += 10;
    // }
    //},
    setHeightToDefault() {
      this.containerHeight = 60;
      // this.charactersLength = 10;
    },
    containerHeightMax() {
      if (this.containerHeight >= 800) {
        this.containerHeight = !this.containerHeight;
      }
    },
    showmorecklick() {
      if (this.windowWidth < 549 && this.containerHeight <= 1000) {
        this.increaseHeight();
        return true;
      } else if (this.windowWidth > 1318 && this.containerHeight <= 500) {
        this.increaseHeight();
        return true;
      }
    },
  },
};
</script>
<style lang="scss" scoped>
@import "./style/styles.scss";
.char-length {
  color: white;
  text-align: center;
  margin-top: 1em;
}
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