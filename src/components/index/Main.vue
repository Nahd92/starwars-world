<template>
  <main class="main bd-grid">
    <!-- Här ska alla delar som ska finnas i main importeras in -->
    <!-- Search part-->

    <Search />
    <Movies :movies="movies" :characters="characters" />
    <Informativ />
    <Character :movies="movies" :characters="characters" />
  </main>
</template>


<script>
import Search from "../search/Search.vue";
import Informativ from "./InformativImage.vue";
import Movies from "../movies/Movies.vue";
import Character from "../character/Characters.vue";
export default {
  name: "Main",
  components: {
    Search,
    Informativ,
    Movies,
    Character,
  },
  data: () => ({
    movies: [],
    characters: [],
    films: [
      {
        src: require("@/assets/movies/a-new-hope.jpg"),
      },
      {
        src: require("@/assets/movies/empire.jpg"),
      },
      {
        src: require("@/assets/movies/return-of-jedi.jpg"),
      },
      {
        src: require("@/assets/movies/the-phantom.jpg"),
      },
      {
        src: require("@/assets/movies/attack-of-the-clones.jpg"),
      },
      {
        src: require("@/assets/movies/revenge-of.jpg"),
      },
    ],
    characterCovers: [
      {
        src: require("@/assets/character/luke2.jpg"),
      },
      {
        src: require("@/assets/character/c-3po.jpeg"),
      },
      {
        src: require("@/assets/character/r2d2.jpeg"),
      },
      {
        src: require("@/assets/character/darthVader.jpg"),
      },
      {
        src: require("@/assets/character/leia.jpg"),
      },
      {
        src: require("@/assets/character/owenLars.jpg"),
      },
      {
        src: require("@/assets/character/beruWhitnesun.jpg"),
      },
      {
        src: require("@/assets/character/r5-d4.jpeg"),
      },
      {
        src: require("@/assets/character/biggsDarklighter.jpeg"),
      },
      {
        src: require("@/assets/character/obi-wan.jpg"),
      },
    ],
    charactersObject: [],
    pages: 1,
  }),
  methods: {
    async fetchAllMovies() {
      const url = "https://swapi.dev/api/films";
      try {
        let movieTemp = [];
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
          const elementUrl = element.url;
          movieTemp.push({
            src,
            title,
            releaseDate,
            producer,
            openingCrawl,
            characters,
            elementUrl,
          });
        }
        this.movies = movieTemp;
      } catch (error) {
        console.log(error);
      }
    },
    async fetchAllCharacters() {
      let data = [];
      try {
        let characterTemp = [];
        do {
          const url = `https://swapi.dev/api/people/?page=${this.pages}`;
          const response = await fetch(url);
          data.push(await response.json());
          this.pages++;
        } while (this.pages <= 9);

        for (let i = 0; i < data.length; i++) {
          this.charactersObject.push(data[i].results);
        }

        for (let i = 0; i < this.charactersObject.length; i++) {
          let charactersArray = this.charactersObject[i];
          for (let y = 0; y < charactersArray.length; y++) {
            const element = charactersArray[y];
            const name = element.name;
            const birthYear = element.birth_year;
            const eyeColor = element.eye_color;
            const url = element.url;
            const films = element.films;
            const characterCover = this.characterCovers[y].src;

            characterTemp.push({
              characterCover,
              name,
              birthYear,
              eyeColor,
              films,
              url,
            });
          }
        }
        this.characters = characterTemp;
      } catch (error) {
        console.log(error);
      }
    },
  },

  async mounted() {
    this.fetchAllMovies();
    this.fetchAllCharacters();
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

.main {
  background-color: var(--dark-color);
  width: 100%;
}
</style>