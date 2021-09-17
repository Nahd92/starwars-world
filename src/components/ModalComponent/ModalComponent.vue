<template>
  <div class="modal-component">
    <transition name="fade">
      <div
        v-if="showModal"
        @click="showModal = false"
        class="modal-overlay"
      ></div>
    </transition>

    <transition name="slide" appear>
      <div v-if="showModal" class="modal">
        <h3>Title: {{ Movies.location }}</h3>
        <h3>Release: {{ Movies.date }}</h3>
        <h3>Episode: {{ Movies.time }}</h3>
        <h3>Movie description:</h3>
        <p>{{ Movies.description }}</p>
        <a class="ModalButton" @click="showModal = false">CLOSE MODAL</a>
      </div>
    </transition>

    <MoviesList v-show="false" v-bind:movies.sync="Movies" />
  </div>
</template>


<script>
import MoviesList from "../MoviesComponent/MoviesListComponent.vue";
export default {
  components: {
    MoviesList,
  },
  name: "ModalComponent",
  data: () => ({
    showModal: false,
    Movies: [],
  }),
  methods: {
    toggleModal() {
      this.showModal = !this.Modal;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";
.modal-component {
  position: relative;

  display: flex;
  justify-content: center;
  align-items: center;

  height: 100vh;
  overflow-wrap: break-word;
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
  background-color: rgba(0, 0, 0, 0.4);
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
  text-align: center;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99;
  height: 80vh;
  width: 100%;
  padding: 25px;
  max-width: 400px;
  background-color: #fff;
  border-radius: 16px;

  a {
    margin: 4em 0;
  }
}
</style>