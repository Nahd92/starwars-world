<template>
  <section class="movieList">
    <h2 class="movieList-title">All Movies</h2>
    <div :style="{ height: containerHeight + 'em' }" class="movieListContainer">
      <!-- Adding v-for here -->
      <div class="movieList-card" v-for="film in movies" v-bind:key="film.id">
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
import ShowMore from "../ShowMoreComponent/ShowMoreComponent.vue";
export default {
  components: {
    ShowMore,
  },
  props: {
    movies: {
      type: Array,
      default: () => [],
    },
  },
  name: "MoviesListComponent",
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
  }),
  methods: {
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
        const src = this.films[i].src;
        this.movies.push({ src, title });
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