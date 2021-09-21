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
              :src="charactersList.characterCover"
              alt="the character image"
              class="modal-image"
            />
          </div>
          <div class="header-info">
            <h3>Name:</h3>
            <p>{{ charactersList.name }}</p>
            <h3>Birth Year:</h3>
            <p>{{ charactersList.birthYear }}</p>
            <h3>Eye color:</h3>
            <p>{{ charactersList.eyeColor }}</p>
          </div>
        </div>

        <div class="description-part">
          <h3 class="description-title">Movies:</h3>
          <div class="description">{{ charactersList.movies }}</div>
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
  props: {
    charactersList: {
      type: Object,
      default: () => [],
    },
  },

  name: "ModalCharacter",
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
    position: absolute;
    bottom: 0;
    right: 0;
    padding: 2.5em;
  }
}
</style>