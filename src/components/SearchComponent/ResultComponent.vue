<!--CHILD -->
<template>
  <div class="result-comp">
    <h3 class="card-title">Search results</h3>
    <div class="card-container bd-grid">
      <div class="card" v-for="film in filteredMovies" v-bind:key="film.id">
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
          <button class="read-more">Read more!</button>
        </div>
      </div>
      <!-- Characters -->
      <div
        class="card"
        v-for="character in filterCharacters"
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
          <button class="read-more">Reade more</button>
        </div>
      </div>
    </div>
    <movies-list-component v-show="false" v-bind:movies.sync="films" />
    <character-list-component
      v-show="false"
      v-bind:charactersList.sync="characters"
    />

    <show-more />
  </div>
</template>

<script>
import CharacterListComponent from "../CharacterComponent/CharacterListComponent.vue";
import MoviesListComponent from "../MoviesComponent/MoviesListComponent.vue";
import ShowMore from "../ShowMoreComponent/ShowMoreComponent.vue";
export default {
  components: {
    MoviesListComponent,
    CharacterListComponent,
    ShowMore,
  },
  name: "searchResultComponent",
  props: {
    searchValue: String,
  },
  data: () => ({
    films: [],
    characters: [],
    newBigArray: [],
  }),
  mounted() {
    for (let i = 0; i < this.characters.length; i++) {
      const element = this.characters[i];
      this.newBigArray.push(element);
    }
  },
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