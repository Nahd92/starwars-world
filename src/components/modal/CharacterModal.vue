<template>
  <div class="modal-component">
    <a class="modal-button" @click="doShowModalCharacter">Read More!</a>

    <transition name="fade">
      <div
        v-if="showModalCharacter"
        @click="showModalCharacter = false"
        class="modal-overlay"
      ></div>
    </transition>

    <transition name="slide" appear>
      <div class="modal" v-if="showModalCharacter">
        <div class="header">
          <div class="image">
            <img
              :src="character.characterCover"
              alt="the character image"
              class="modal-image"
            />
          </div>
          <div class="header-info">
            <h3>Name:</h3>
            <p>{{ character.name }}</p>
            <h3>Birth Year:</h3>
            <p>{{ character.birthYear }}</p>
            <h3>Eye color:</h3>
            <p>{{ character.eyeColor }}</p>
          </div>
        </div>

        <div class="movies-images">
          <h3 class="movies-title">Characters in the Movie</h3>
          <div class="movies-container">
            <div
              class="movies"
              v-for="movie in filterAllMovies"
              v-bind:key="movie.id"
            >
              <div class="movies-card-img">
                <h4>{{ movie.title }}</h4>
                <img :src="movie.src" alt="character in movie" />
              </div>
            </div>
          </div>
        </div>

        <div class="closebtn">
          <a class="modal-button" @click="doNotshowCharacterModal"
            >CLOSE MODAL</a
          >
        </div>
      </div>
    </transition>
  </div>
</template>


<script>
export default {
  name: "CharacterModal",
  props: {
    character: {
      type: Object,
      default: () => ({}),
    },
    movies: {
      type: Array,
      default: () => [],
    },
  },

  data: () => ({
    showModalCharacter: false,
    Characters: [],
    films: [],
  }),
  methods: {
    doShowModalCharacter() {
      this.showModalCharacter = true;
    },
    doNotshowCharacterModal() {
      this.showModalCharacter = false;
    },
  },
  computed: {
    filterAllMovies: function () {
      return this.movies.filter((movie) => {
        return this.character.films.find((charactersUrl) => {
          console.log("movie", movie.elementUrl);
          console.log("character", charactersUrl);
          return charactersUrl === movie.elementUrl;
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
  h4 {
    font-size: 0.8em;
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

.movies-images {
  .movies-title {
    color: var(--white-color);
    text-align: center;
    margin: 1em 0;
  }

  .movies-container {
    width: 100%;
    display: flex;
    flex-direction: row;
    overflow: auto;
    justify-content: flex-start;
    align-items: center;
  }
  .movies {
    .movies-card-img {
      width: 10em;
      margin: 0.3em 0.4em;
      display: flex;
      flex-direction: column;
      justify-content: center;
      position: relative;
      align-items: center;

      img {
        width: 100%;
        height: 7em;
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
  height: 80vh;
  width: 100%;
  padding: 25px;
  max-width: 800px;
  background-color: var(--dark-color);
  border-radius: 16px;

  -webkit-box-shadow: 2px 5px 16px 0px #0b325e,
    50px 50px 50px 50px rgba(145, 145, 145, 0),
    50px 50px 50px 50px rgba(145, 145, 145, 0);
  box-shadow: 2px 5px 16px 0px #0b325e,
    50px 50px 50px 50px rgba(145, 145, 145, 0),
    50px 50px 50px 50px rgba(145, 145, 145, 0);

  .image {
    width: 100%;
    height: 30vh;
    overflow: hidden;

    .modal-image {
      width: 100%;
    }
  }

  .header {
    display: flex;
    justify-content: space-around;

    .header-info {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      width: 100%;
      padding: 0 2em;
      height: 12.6em;
      h3,
      p {
        color: white;
      }

      p {
        font-size: 0.7;
      }
    }
  }
  .description-part {
    height: 20em;
    margin-top: 3em;

    .description-title {
      color: white;
    }

    .description {
      color: white;
      padding: 2em;
      line-height: 2em;
    }
  }

  .closebtn {
    display: flex;
    justify-content: center;
    .modal-button {
      position: relative;
      bottom: 1em;
    }
  }
}
@media screen and (max-width: 320px) {
  .modal {
    width: 90%;
    height: 20em;
    .image {
      width: 40em;

      .modal-image {
        width: 100%;
        height: 8em;
      }
    }
    .header {
      .header-info {
        font-size: 0.6em;
        h3,
        p {
          color: white;
        }

        p {
          font-size: 0.7;
        }
      }
    }
    .closebtn {
      display: flex;
      justify-content: center;
      .modal-button {
        position: relative;
        bottom: 1em;
      }
    }
  }
}
@media screen and (max-width: 550px) {
  .modal {
    .image {
      width: 50em;

      .modal-image {
        width: 100%;
        height: 10em;
      }
    }
    .header-info {
      font-size: 0.8em;
      h3,
      p {
        color: white;
      }

      p {
        font-size: 0.7;
      }
    }
  }
}
</style>