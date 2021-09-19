<template>
  <section class="characterList">
    <h2 class="character-title">All Character</h2>
    <div
      :style="{ height: containerHeight + 'em' }"
      class="character-container"
    >
      <div
        class="character-card"
        v-for="(character, index) in fetchCharacters"
        v-bind:key="character.id"
      >
        <div class="character-img">
          <img :src="character.characterCover" alt="luke" />
        </div>
        <div class="character-information">
          <h2>Name</h2>
          <h3 class="character-name">{{ character.name }}</h3>
         
        </div>
        <div class="card-button"  >
          <Modal :charactersList="charactersList[index]"/>
        </div>
      </div>
    </div>

    />
  </section>
</template>
<script>
import Modal from "../ModalComponent/ModalCharacter.vue"
import ShowMore from "../ShowMoreComponent/ShowMoreComponent.vue";
export default {
  components: {
    ShowMore,
    Modal
   

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
          const movies = element.films
         
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
            eyeColor,movies
          });
         
          
        }
        
      }
     
       this.$emit("update:characters",this.charactersList);
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
.character-information h2 {
  font-size: 20px;
  opacity: 0.5;
}

.character-title {
  text-align: center;
}

.character-title {
  font-size: 3em;
}
.character-container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-evenly;
  overflow: hidden;

  .character-card {
    background-color: black;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 17em;

    margin: 1em 1em;
    border-radius: 0.5em;
    -webkit-box-shadow: 2px 5px 16px 0px #0b325e,
      50px 50px 50px 50px rgba(145, 145, 145, 0),
      50px 50px 50px 50px rgba(145, 145, 145, 0);
    box-shadow: 2px 5px 16px 0px #0b325e,
      50px 50px 50px 50px rgba(145, 145, 145, 0),
      50px 50px 50px 50px rgba(145, 145, 145, 0);

    .character-img {
      background-color: var(--white-color);
      width: 94%;
      margin: 0.5em 0;

      img {
        border-radius: 0.5em;
        width: 17em;
        height: 11em;
      }
    }

    .character-information {
      text-align: center;
      width: 100%;
      margin-top: 1em;

      h3 {
        font-size: 1em;
        font-weight: normal;
        color: white;
      }
    }
    /*

    &:hover {
      -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff,
        2px 5px 16px 0px #0b325e, 5px 5px 15px 5px rgba(0, 0, 0, 0);
      box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
        5px 5px 15px 5px rgba(0, 0, 0, 0);
      transform: scale(1.1);
    }*/

    .card-button {
      cursor: pointer;
      margin-top: 1.5em;
      margin-bottom: 1.5em;

      .read-more {
        font-size: 1.2em;
        padding: 0.7em;
        border-radius: 1em;
        background: rgba(31, 135, 255, 0.7);
        color: white;
         
        &:hover {
          -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff,
            2px 5px 16px 0px #0b325e, 5px 5px 15px 5px rgba(0, 0, 0, 0);
          box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
            5px 5px 15px 5px rgba(0, 0, 0, 0);
          transform: scale(1.05);
          color: white;
          opacity: 1;
        }
      }
    }
  }
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