<template>
  <section class="movieList bd-grid">
    <h2 class="movieList-title">All Movies</h2>
    <div class="movieList-container">
      <!-- Adding v-for here -->
      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>

      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>

      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>

      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>

      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>
      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>
      <div class="movieList-card">
        <div class="movie-img">
          <!-- Adding src by binding here -->
          <img src="../../assets/galaxy.jpg" alt="Helmet" />
        </div>
        <div class="movie-information">
          <h3 class="card-text">
            STAR WARS <br />
            GALAXY OF HEROES {{ /* Title */}}
          </h3>
        </div>
        <div class="card-button">
          <button class="read-more">Read more!</button>
        </div>
      </div>

      <div class="cards-overlay"></div>
    </div>
  </section>
</template>

<script>
export default {
  name: "MoviesListComponent",
  data: () => ({
    films: [],
    filmImages: {},
  }),
  async mounted() {
    const url = "https://swapi.dev/api/films";
    try {
      const response = fetch(url);
      const data = await response.json();
    } catch (error) {}
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";

h3,
p {
  color: black;
}

.cards-overlay {
  position: absolute;
  height: 100vh;
  margin-top: 40em;
  width: 50%;
  background-color: var(--dark-color);
}

.movieList-title {
  text-align: center;
}

.movieList-title {
  font-size: 3em;
}
.movieList-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
  margin-top: 3em;

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
</style>