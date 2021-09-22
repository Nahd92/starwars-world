<!--CHILD -->
<template>
  <div class="result-comp">
    <h3 class="card-title search-title">Search results</h3>
    <div class="card-container">
      <p
        class="couldNotUnderstand"
        v-if="filteredMovies.length === 0 && filterCharacters.length === 0"
      >
        Could not understand that search, try again!
      </p>
      <div
        v-else
        class="card"
        v-for="(film, index) in filteredMovies"
        v-bind:key="film.id"
      >
        <div class="card-img">
          <!-- Adding src by binding here -->
          <img :src="film.src" alt="Helmet" />
        </div>
        <div class="card-information">
          <h3 class="card-text">
            {{ film.title }}
          </h3>
        </div>
        <div class="card-button">
          <Modal :movie="films[index]" />
        </div>
      </div>

      <!-- Characters -->
      <div
        class="card"
        v-for="(character, index) in filterCharacters"
        v-bind:key="character.id"
      >
        <div class="card-img">
          <img :src="character.characterCover" alt="luke" />
        </div>
        <div class="card-information">
          <h3 class="character-name">{{ character.name }}</h3>
          <h3 class="character-age">{{ character.birthYear }}</h3>
          <h3 class="character-eyes">{{ character.eyeColor }}</h3>
        </div>
        <div class="card-button">
          <ModalCharacter :charactersList="filterCharacters[index]" />
        </div>
      </div>
    </div>
    <movies-list-component v-show="false" v-bind:movies.sync="films" />
    <Characters v-show="false" v-bind:charactersList.sync="characters" />
  </div>
</template>

<script>
import Modal from "../modal/MoviesModal.vue";
import ModalCharacter from "../modal/CharacterModal.vue";
import Characters from "../character/Characters.vue";
import MoviesListComponent from "../movies/Movies.vue";
export default {
  components: {
    MoviesListComponent,
    Characters,
    Modal,
    ModalCharacter,
  },
  name: "Result",
  props: {
    searchValue: String,
  },
  data: () => ({
    films: [],
    characters: [],
  }),

  computed: {
    filteredMovies: function () {
      return this.films.filter((movie) => {
        return movie.title
          .toLowerCase()
          .includes(this.searchValue.toLowerCase());
      });
    },
    filterCharacters: function () {
      return this.characters.filter((character) => {
        return character.name
          .toLowerCase()
          .includes(this.searchValue.toLowerCase());
      });
    },
  },
};
</script>




<style lang="scss" scoped>
@import "./style/styles.scss";

h3,
p {
  color: white;
}

.search-title {
  margin-top: 0.3em;
}
.card-container {
  height: auto;
  border-bottom: solid 1px #fff;
  margin-bottom: 3em;
  overflow: visible;

  .couldNotUnderstand {
    margin: 5em 0;
  }

  .card {
    width: 14em;
  }
}
@media screen and (min-width: 727px) {
}
@media screen and (min-width: 1024px) {
}
</style>