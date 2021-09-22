<template>
  <section>
    <h2 class="card-title">All Movies</h2>
    <div :style="{ height: containerHeight + 'em' }" class="card-container">
      <!-- Adding v-for here -->
      <div
        class="card"
        v-for="(film, index) in fetchedFilms"
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
          <Modal :movie="movies[index]" />
        </div>
      </div>
    </div>

    {{ windowWidth }}

    <!-- mindre än 530  Mobile 165 -->
    <!--  530  tablet 80 -->
    <!-- 910 bredd Smaller Desktop 55 -->

    <!--PARENT-->
    <div class="show-more-cont">
      <ShowMore
        v-if="changeShowButtonFunctionalityOnMediaScreen"
        v-on:showMore="increaseHeight()"
      />
      <ShowMore
        v-else
        aria-disabled="true"
        v-on:showNotMore="setHeightToDefault()"
      />
    </div>
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
        src: require("@/assets/a-new-hope.jpg"),
      },
      {
        src: require("@/assets/empire.jpg"),
      },
      {
        src: require("@/assets/return-of-jedi.jpg"),
      },
      {
        src: require("@/assets/the-phantom.jpg"),
      },
      {
        src: require("@/assets/attack-of-the-clones.jpg"),
      },
      {
        src: require("@/assets/revenge-of.jpg"),
      },
    ],
    containerHeight: 32,
    containerMaxHeight: false,
    fetchedFilms: [],
  }),
  methods: {
    toggleCardHover() {
      this.cardHover = !this.cardHover;
    },
    increaseHeight() {
      this.containerHeight += 27;
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
  computed: {
    changeShowButtonFunctionalityOnMediaScreen() {
      console.log(this.windowWidth);
      if (this.windowWidth < 549 && this.containerHeight <= 165) {
        console.log("mobile true");
        return true;
      } else if (
        this.windowWidth > 550 &&
        this.windowWidth < 929 &&
        this.containerHeight <= 80
      ) {
        console.log("tablet, true");
        return true;
      } else if (this.windowWidth > 915 && this.containerHeight <= 55) {
        console.log("Desktop, true");
        return true;
      } else {
        console.log("false");
        return false;
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
          url,
        });
      }
      this.$emit("update:movies", this.movies);
    } catch (error) {
      console.log("error från movieList", error);
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

@media screen and (max-width: 727px) {
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