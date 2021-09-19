<!--CHILD -->
<template>
  <div class="searchResult">
    <h3 class="SearchResult-title">Search results</h3>
    <div class="searchResult-container bd-grid">
      <div
        class="movieList-card"
        v-for="film in filteredMovies"
        v-bind:key="film.id"
      >
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img :src="film.src" alt="Helmet" />
        </div>
        <div class="movie-information">
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
        class="character-card"
        v-for="character in filterCharacters"
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
    <movies-list-component v-show="false" v-bind:movies.sync="films" />
    <character-list-component
      v-show="false"
      v-bind:charactersList.sync="characters"
    />
  </div>
</template>

<script>
import CharacterListComponent from "../CharacterComponent/CharacterListComponent.vue";
import MoviesListComponent from "../MoviesComponent/MoviesListComponent.vue";
export default {
  components: {
    MoviesListComponent,
    CharacterListComponent,
  },
  name: "searchResultComponent",
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
  color: black;
}

.SearchResult-title {
  text-align: center;
  font-size: 2em;
  color: white;
}
.movieList-title {
  text-align: center;
}
.movieList-title {
  font-size: 3em;
}

.searchResult-container {
  height: 50vh;
  color: red;
  margin-bottom: 10em;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-evenly;
  overflow: hidden;
  border-bottom: solid 2px grey;
  .movieList-card {
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
    .movie-img {
      background-color: var(--white-color);
      width: 94%;
      margin: 0.5em 0;
      img {
        border-radius: 0.5em;
      }
    }
    .movie-information {
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

.character-title {
  text-align: center;
}

.character-title {
  font-size: 3em;
}
.searchResult-container {
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