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

        <div class="characters-images">
          <h3 class="chars-title">Characters in the Movie</h3>
          <div class="characters-container">
            <div
              class="characters"
              v-for="(character, index) in filterAllCharacters"
              v-bind:key="character.id"
            >
              <div class="char-card-img">
                <img :src="character.characterCover" alt="character in movie" />
                <div class="read-more-container">
                  <CharacterModal
                    :charactersList="filterAllCharacters[index]"
                  />
                </div>
              </div>
            </div>
          </div>
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
import CharacterModal from "../ModalComponent/ModalCharacter.vue";
export default {
  components: {
    CharacterModal,
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
  },
  computed: {
    filterAllCharacters: function () {
      return this.characters.filter((char) => {
        return this.movie.characters.find((movieCharUrl) => {
          return movieCharUrl === char.url;
        });
      });
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
  margin-top: 2em;
  margin-bottom: 0px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99;
  height: 95%;
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
    justify-content: space-around;
    .image-container {
      width: 40%;
    }

    .header-info {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      padding: 0 2em;

      width: 100%;

      height: 10.6em;
      h3,
      p {
        font-size: 95%;
        color: white;
      }
    }
  }
  .description-part {
    height: 20em;
    margin-top: 1.5em;
    padding: 0 2em;

    .description-title {
      color: white;
    }

    .description {
      color: white;
      font-size: 0.9em;
    }
  }

  .characters-images {
    .chars-title {
      color: var(--white-color);
      text-align: center;
      margin: 1em 0;
    }

    .characters-container {
      width: 100%;
      display: flex;
      flex-direction: row;
      overflow: auto;
      justify-content: flex-start;
      align-items: center;
      ::-webkit-scrollbar-track {
        background-color: #333;
      }
    }
    .characters {
      .char-card-img {
        width: 10em;
        margin: 0em 0.4em;
        display: flex;
        flex-direction: column;
        justify-content: center;
        position: relative;
        align-items: center;

        img {
          width: 10em;
          height: 10em;
        }

        .read-more-container {
          position: absolute;
          overflow: hidden;
          bottom: 0;
          right: 0;
          left: 0;
          margin-bottom: 0.5em;

          .read-more-button {
            font-size: 0.8em;
            opacity: 0.8;

            &:hover {
              opacity: 1;
            }
          }
        }
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
/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
@media screen and (min-width: 848px) {
  .modal {
    width: 70%;
    height: 75vh;
    .header {
      .image-container {
        width: 40%;
      }
      .image-container img {
        width: none;
        height: none;
      }
      .header-info {
        display: flex;
        flex-direction: column;
        align-items: center;

        width: 100%;
        padding: 0 2em;
        height: 10.6em;
        h3,
        p {
          color: white;
        }
      }
    }
  }
}
@media screen and (min-width: 1024px) {
  .modal {
    width: 100%;
    max-width: 1300px;
    .header {
      display: flex;
      justify-content: space-around;
      .image-container {
        width: 30%;
      }

      .header-info {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding: 0 2em;

        width: 100%;
      }
    }
  }
}
</style>