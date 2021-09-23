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
                    :character="filterAllCharacters[index]"
                    :movies="movies"
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
  </div>
</template>


<script>
import CharacterModal from "./CharacterModal.vue";
export default {
  components: {
    CharacterModal,
  },
  props: {
    movies: {
      type: Array,
      default: () => [],
    },
    movie: {
      type: Object,
      default: () => ({}),
    },
    characters: {
      type: Array,
      default: () => [],
    },
  },
  name: "MoviesModal",
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
    }
    .characters {
      .char-card-img {
        width: 10em;
        margin: 0.3em 0.4em;
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
::-webkit-scrollbar-track {
  background-color: #333;
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

@media screen and (max-width: 375px) {
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 98;
    background-color: rgba(0, 0, 0, 0.8);
  }

  .modal {
    width: 100%;
    height: 100vh;
    overflow: auto;
    .header {
      display: flex;
      justify-content: center;
      align-items: center;
      .image-container {
        width: 60%;
      }
      .header-info {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        word-wrap: break-word;
        width: 100%;
        padding: 0 1em;
        text-align: center;
        margin-top: 0.5em;

        h3,
        p {
          color: white;
          font-size: 0.8em;
        }
      }
    }
    .closebtn {
      position: relative;
      .modal-button {
        position: absolute;
        bottom: 0;
        margin: 0.7em 0;
        right: 0;
      }
    }
  }
}

@media screen and (min-width: 848px) {
  .modal {
    width: 75%;
    height: 80vh;
    .header {
      .image-container {
        width: 50%;
      }
      .headerInfo {
        padding: 0;
        width: 50%;
        .header-info {
          padding: 0;
          text-align: center;
          display: flex;
          align-items: center;
          h3,
          p {
            color: white;
          }
        }
      }
    }
    .closebtn {
      .modal-button {
        position: absolute;
        bottom: 0;
        right: 0;
        margin: 0 1em 0.3em 0;
      }
    }
  }
}
@media screen and (min-width: 1024px) {
  .modal {
    height: 90vh;
    width: 70%;
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