<template>
  <section>
    <h2 class="card-title characters-title">All Character</h2>
    <div :style="{ height: containerHeight + 'em' }" class="card-container">
      <div
        class="card"
        v-for="(character, index) in fetchCharacters"
        v-bind:key="character.id"
      >
        <div class="card-img">
          <img :src="character.characterCover" alt="luke" />
        </div>
        <div class="card-information">
          <h2>Name</h2>
          <h3 class="card-name">{{ character.name }}</h3>
        </div>
        <div class="card-button">
          <Modal :charactersList="charactersList[index]" />
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
import Modal from "../ModalComponent/ModalCharacter.vue";
import ShowMore from "../ShowMoreComponent/ShowMoreComponent.vue";
export default {
  components: {
    ShowMore,
    Modal,
  },
  props: {
    charactersList: {
      type: Array,
      default: () => [],
    },
  },
  name: "CharacterListComponent",
  data: () => ({
    characterCovers: [
      {
        src: require("@/assets/luke2.jpg"),
      },
      {
        src: require("@/assets/character/c-3po.jpeg"),
      },
      {
        src: require("@/assets/character/r2d2.jpeg"),
      },
      {
        src: require("@/assets/character/darthVader.jpg"),
      },
      {
        src: require("@/assets/character/leia.jpg"),
      },
      {
        src: require("@/assets/character/owenLars.jpg"),
      },
      {
        src: require("@/assets/character/beruWhitnesun.jpg"),
      },
      {
        src: require("@/assets/character/r5-d4.jpeg"),
      },
      {
        src: require("@/assets/character/biggsDarklighter.jpeg"),
      },
      {
        src: require("@/assets/character/obi-wan.jpg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
    ],
    fetchcovers: [],
    fetchCharacters: [],
    textIsVisible: true,
    pages: 1,
    containerHeight: 32,
    containerMaxHeight: false,
    charactersObject: [],
  }),

  methods: {
    increaseHeight() {
      this.containerHeight += 30;
    },
    setHeightToDefault() {
      this.containerHeight = 32;
    },
    containerHeightMax() {
      if (this.containerHeight >= 100) {
        this.containerHeight = !this.containerHeight;
      }
    },
    showText() {
      console.log("den körs");
      this.textIsVisible = !this.textIsVisible;
    },
  },

  async created() {
    let data = [];
    try {
      do {
        const url = `https://swapi.dev/api/people/?page=${this.pages}`;
        const response = await fetch(url);
        data.push(await response.json());
        this.pages++;
      } while (this.pages <= 9);

      for (let i = 0; i < data.length; i++) {
        this.charactersObject.push(data[i].results);
      }

      for (let i = 0; i < this.charactersObject.length; i++) {
        let charactersArray = this.charactersObject[i];
        for (let y = 0; y < charactersArray.length; y++) {
          const element = charactersArray[y];
          const name = element.name;
          const birthYear = element.birth_year;
          const eyeColor = element.eye_color;
          const movies = element.films;

          const characterCover = this.characterCovers[y].src;
          this.fetchCharacters.push({
            characterCover,
            name,
            birthYear,
            eyeColor,
          });
          this.charactersList.push({
            characterCover,
            name,
            birthYear,
            eyeColor,
            movies,
          });
        }
      }

      this.$emit("update:characters", this.charactersList);
    } catch (error) {
      console.log(error);
    }
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

@media screen and (min-width: 727px) {
}

@media screen and (min-width: 1024px) {
  .character-container {
    display: flex;

    .character-card {
      padding: 0.5em;
    }
  }
}
</style>