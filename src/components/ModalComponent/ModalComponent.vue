<template>
  <div class="modal-component">
    <a class="modal-button" @click="doShowModal">Read More!</a>

    <transition name="fade">
      <div
        v-if="showModal"
        @click="showModal = false"
        class="modal-overlay"
      ></div>
    </transition>

    <transition name="slide" appear>
      <div class="modal" v-if="showModal">
        <div class="header">
          <div class="image-container">
            <div class="image">
              <img
                :src="movie.src"
                alt="the movies image"
                class="modal-image"
              />
            </div>
          </div>
          <div class="headerInfo">
            <div class="header-info">
              <h3>Title:</h3>
              <p>{{ movie.title }}</p>
              <h3>Producer:</h3>
              <p>{{ movie.producer }}</p>
              <h3>Released:</h3>
              <p>{{ movie.releaseDate }}</p>
            </div>
          </div>
        </div>

        <h3 class="chars-title">Characters in the Movie</h3>

        <transition-group name="fade" tag="div">
          <div
            class="characters"
            v-for="character in filterAllCharacters"
            v-bind:key="character.id"
          >
            <div class="char-card-img">
              <img :src="character.characterCover" alt="character in movie" />
            </div>
          </div>
        </transition-group>

        <div class="images-carousell-arrows">
          <i
            class="bx bx-left-arrow-alt arrow-icon"
            v-bind:disabled="currentIndex < 1"
            @click="prev"
          ></i>
          <i
            class="bx bx-right-arrow-alt arrow-icon"
            v-bind:disabled="currentIndex == movie.characters.length - 1"
            @click="next"
          ></i>
        </div>

        <div class="description-part">
          <h3 class="description-title">Description:</h3>
          <div class="description">{{ movie.openingCrawl }}</div>
        </div>

        <div class="closebtn">
          <a class="modal-button" @click="doNotshowModal">CLOSE </a>
        </div>
      </div>
    </transition>

    <character-list-component
      v-show="false"
      v-bind:charactersList.sync="characters"
    />
  </div>
</template>


<script>
import CharacterListComponent from "../CharacterComponent/CharacterListComponent.vue";
export default {
  components: {
    CharacterListComponent,
  },
  props: {
    movie: {
      type: Object,
      default: () => ({}),
    },
    characters: {
      type: Array,
      default: () => [],
    },
  },
  name: "ModalComponent",
  data: () => ({
    showModal: false,
    movieCharacters: [],
    transitionSlide: "",
    currentIndex: 0,
  }),
  methods: {
    doShowModal() {
      this.showModal = true;
    },
    doNotshowModal() {
      this.showModal = false;
    },
    next() {
      if (this.currentIndex < 3) {
        console.log("next");
        this.currentIndex += 1;
      } else {
        this.currentIndex = 0;
      }
    },
    prev() {
      console.log("prev");
      this.currentIndex -= 1;
    },
  },
  computed: {
    filterAllCharacters: function () {
      return this.characters.filter((char) => {
        return this.movie.characters.find((movieCharUrl) => {
          //console.log("FilterAllCharacters, Modal", movieCharUrl, char.url);
          return movieCharUrl === char.url;
        });
      });
    },
    currentImg() {
      return this.movie.characters[
        Math.abs(this.currentIndex) % this.movie.characters
      ];
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.modal-component {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  a,
  p,
  h1,
  h3 {
    color: blacK;
  }
}
.modal-button {
  font-size: 1.2em;
  margin-top: 2em;
  padding: 0.7em;
  border-radius: 1em;
  background: rgba(31, 135, 255, 0.7);
  color: white;
  cursor: pointer;

  &:hover {
    -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
      5px 5px 15px 5px rgba(0, 0, 0, 0);
    box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
      5px 5px 15px 5px rgba(0, 0, 0, 0);
    transform: scale(1.05);
    color: white;
    opacity: 1;
  }
}

.modal-header-info {
  text-align: left;
  margin: 2em 0;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 98;
  background-color: rgba(0, 0, 0, 0.8);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave {
  opacity: 0;
}

.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99;
  height: 75vh;
  width: 100%;
  padding: 25px;
  max-width: 1000px;
  background-color: var(--dark-color);
  border-radius: 16px;

  -webkit-box-shadow: 2px 5px 16px 0px #0b325e,
    50px 50px 50px 50px rgba(145, 145, 145, 0),
    50px 50px 50px 50px rgba(145, 145, 145, 0);
  box-shadow: 2px 5px 16px 0px #0b325e,
    50px 50px 50px 50px rgba(145, 145, 145, 0),
    50px 50px 50px 50px rgba(145, 145, 145, 0);

  .header {
    display: flex;
    justify-content: space-evenly;
    align-items: center;

    .image-container {
      width: 30%;
    }

    .header-info {
      display: flex;
      flex-direction: column;

      width: 100%;
      padding: 0 2em;
      height: 10.6em;
      h3,
      p {
        color: white;
      }

      p {
        font-size: 0.5;
      }
    }
  }
  .description-part {
    height: 20em;
    margin-top: 1em;

    .description-title {
      color: white;
    }

    .description {
      color: white;
      padding: 0em;
      line-height: 2em;
    }
  }

  .chars-title {
    color: var(--white-color);
    text-align: center;
    margin: 1em 0;
  }

  .characters {
    display: flex;
    align-items: center;
    flex-direction: row;
    white-space: nowrap;
    overflow: hidden;
    .char-card-img {
      width: 10em;
      margin: 0 0.4em;
    }
  }
  .images-carousell-arrows {
    text-align: center;
    font-size: 2em;
    color: grey;

    .arrow-icon {
      cursor: pointer;
      padding: 0 0.3em;

      &:hover {
        color: white;
        transform: scale(1.1);
      }
    }
  }

  .closebtn {
    position: absolute;
    bottom: 0;
    right: 0;
    padding: 2.5em;
  }
}
</style>