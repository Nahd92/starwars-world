<template>
  <section class="movieList">
    <h2 class="movieList-title">All Movies</h2>
    <div :style="{ height: containerHeight + 'em' }" class="movieListContainer">
      <!-- Adding v-for here -->
      <div
        class="movieList-card"
        v-for="(film, index) in fetchedFilms"
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
          <Modal :movie="movies[index]" />
        </div>
      </div>
    </div>

    <!--PARENT-->
    <ShowMore
      v-show="containerHeight <= 80"
      v-if="containerHeight <= 32"
      v-on:showMore="increaseHeight()"
    />
    <ShowMore
      v-else
      aria-disabled="true"
      v-on:showNotMore="setHeightToDefault()"
    />
  </section>
</template>

<script>
import Modal from "../ModalComponent/ModalComponent.vue";
import ShowMore from "../ShowMoreComponent/ShowMoreComponent.vue";
export default {
  name: "MoviesListComponent",
  components: {
    Modal,
    ShowMore,
  },
  props: {
    movie: {
      type: Object,
      default: () => ({}),
    },
    movies: {
      type: Array,
      default: () => [],
    },
  },
  data: () => ({
    films: [
      {
        src: require("@/assets/galaxy.jpg"),
      },
      {
        src: require("@/assets/luke2.jpg"),
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
        src: require("@/assets/galaxy.jpg"),
      },
    ],
    containerHeight: 32,
    containerMaxHeight: false,
    fetchedFilms: [],
    cardHover: true,
  }),
  methods: {
    toggleCardHover() {
      this.cardHover = !this.cardHover;
    },
    increaseHeight() {
      this.containerHeight += 25;
    },
    setHeightToDefault() {
      this.containerHeight = 32;
    },
    containerHeightMax() {
      if (this.containerHeight >= 82) {
        this.containerHeightMax = !this.containerHeight;
      }
    },
  },
  async mounted() {
    const url = "https://swapi.dev/api/films";
    try {
      const response = await fetch(url);
      const data = await response.json();
      for (let i = 0; i < data.results.length; i++) {
        const element = data.results[i];
        const title = element.title;
        const releaseDate = element.release_date;
        const producer = element.producer;
        const openingCrawl = element.opening_crawl;
        const characters = element.characters;

        const src = this.films[i].src;

        this.fetchedFilms.push({
          src,
          title,
          releaseDate,
          producer,
          openingCrawl,
          characters,
        });
        this.movies.push({
          src,
          title,
          releaseDate,
          producer,
          openingCrawl,
          characters,
        });
      }
      this.$emit("update:movies", this.movies);
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
.movieList-title {
  text-align: center;
}
.movieList-title {
  font-size: 3em;
}

.movieListContainer {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-evenly;
  overflow: hidden;
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
    /*
    &:hover {
      -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff,
        2px 5px 16px 0px #0b325e, 5px 5px 15px 5px rgba(0, 0, 0, 0);
      box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
        5px 5px 15px 5px rgba(0, 0, 0, 0);
      transform: scale(1.1);
    }
    */
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