<template>
  <section class="characterList">
    <h2 class="character-title">All Character</h2>
    <div :style="{ height: containerHeight + 'em' }" class="character-container">
      <div
        class="character-card"
        v-for="character in fetchCharacters"
        v-bind:key="character.id"
      >
        <div class="character-img">
          <img :src="character.characterCover" alt="luke" />
        </div>
        <div class="character-information">
          <h3 class="character-name">{{ character.name }}</h3>
          <h3 class="character-age">{{ character.birthYear }}</h3>
          <h3 class="character-eyes">{{ character.eyeColor }}</h3>
        </div>
        <div class="card-button">
          <button class="read-more">Reade more</button>
        </div>
      </div>
    </div>
   
    
    <!--PARENT-->
     <ShowMore
       v-on:showMore="increaseHeight()"
       v-on:showNotMore="setHeightToDefault()"

    /> 
   
  </section>
</template>
<script>
import ShowMore from "../ShowMoreComponent/ShowMoreComponent.vue";
export default {
  components:{
    ShowMore

  },
  name: "CharacterListComponent",
  data: () => ({
    characterCovers: [
      {
        src: require("@/assets/luke2.jpg"),
      },
      {
        src: require("@/assets/c-3po.jpeg"),
      },
      {
        src: require("@/assets/r2d2.jpeg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/luke2.jpg"),
      },
      {
        src: require("@/assets/c-3po.jpeg"),
      },
      {
        src: require("@/assets/r2d2.jpeg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/galaxy.jpg"),
      },
    ],
    
    fetchCharacters: [],
    
    pages: 1,
    containerHeight: 32,
    containerMaxHeight: false,
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
   
   
  },
  computed: {},

  async mounted() {
    let data = [];
    try {
      do {
        const pages = `https://swapi.dev/api/people/?page=${this.pages}`;
        const response = await fetch(pages);
        data.push(await response.json());
        this.pages++;
      } while (this.pages <= 9);

      let charactersObject = [];

      for (let i = 0; i < data.length; i++) {
        charactersObject.push(data[i].results);
      }

      for (let i = 0; i < charactersObject.length; i++) {
        let charactersArray = charactersObject[i];
        for (let y = 0; y < charactersArray.length; y++) {
          const element = charactersArray[y];
          const name = element.name;
          const birthYear = element.birth_year;
          const eyeColor = element.eye_color;
          const characterCover = this.characterCovers[y].src;
          this.fetchCharacters.push({
            characterCover,
            name,
            birthYear,
            eyeColor,
          });
        }
      }
    } catch (error) {}
  },
};
</script>
<style lang="scss" scoped>
@import "./style/styles.scss";

.next{
  position: relative;


}
h3,
p {
  color: black;
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
    height: 25em;
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
      margin-top: 2em;

      h3 {
        font-size: 1em;
        font-weight: normal;
        color: white;
      }
    }

    &:hover {
      -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff,
        2px 5px 16px 0px #0b325e, 5px 5px 15px 5px rgba(0, 0, 0, 0);
      box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
        5px 5px 15px 5px rgba(0, 0, 0, 0);
      transform: scale(1.1);
    }

    .card-button {
      margin-top: 2.5em;

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
  .movieListContainer {
    display: flex;

    .movieList-card {
      padding: 0.5em;
    }
  }
}
</style>