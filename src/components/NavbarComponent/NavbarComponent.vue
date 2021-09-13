<template>
  <div class="nav">
    <div class="left-grid-logo">
      <a href="#" class="nav-logo">STAR WARS WORLD</a>
    </div>

    <!-- NAVBAR -->
    <transition name="fade">
      <div
        v-show="isExpanded"
        :class="{ showMenu: isExpanded ? 'showMenu' : 'nav__menu' }"
      >
        <ul class="nav-list">
          <li class="nav-item"><a href="#" class="nav-link">EVENTS</a></li>
          <li class="nav-item"><a href="#" class="nav-link">NEWS</a></li>
          <li class="nav-item"><a href="#" class="nav-link">GALLERY</a></li>
          <li class="nav-item"><a href="#" class="nav-link">ABOUT</a></li>
          <li class="nav-item"><a href="#" class="nav-link">CONTACT</a></li>
        </ul>
      </div>
    </transition>
    <div class="nav__toggle" @click="toggleMenu">
      <i class="bx bx-grid-alt"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavbarComponent",
};
</script>

<style lang="scss" scoped>
/* === NAV   === */
.nav {
  height: var(--header-height-bigger);
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-content: space-between;
  padding-top: 10px;
  padding: 10px 2em 2em 0;
  background: transparent;
  margin: 0;
  width: 100%;
  background-color: var(--dark-color);
  box-shadow: 5px -1px 12px -5px grey;
  opacity: 1;
}

.nav-item {
  margin-bottom: var(--mb-4);
}

.nav-item:hover {
  opacity: 1;
}

.nav__toggle {
  font-size: 1.7rem;
  cursor: pointer;
  color: white;
}

.nav-logo {
  font-weight: var(--font-semi-bold);
  font-size: 1rem;
  color: white;
  padding: 1em;
  cursor: pointer;
  line-height: 2.3em;
}

.nav__search {
  font-size: 1.7rem;
  color: white;
  margin-right: 1em;
  cursor: pointer;
}

.left-grid-logo {
  height: 10px;
  width: 20em;
}

.left-grid-logo:hover {
  transform: scale(1.07);
}

.nav__toggle:hover,
.nav__search:hover {
  transform: scale(1.07);
}

.signup {
  display: none;
  color: white;
}

.signup:hover {
  transform: scale(1.04);
}

@media screen and (max-width: 1024px) {
  .nav__menu {
    position: fixed;
    top: var(--header-height-bigger);
    right: -100%;
    width: 40%;
    height: 100vh;
    padding: 2rem;
    background-color: var(--dark-color);
    font-size: 15px;
    transition: 0.3s;
  }
  .showMenu {
    position: fixed;
    top: var(--header-height-bigger);
    right: 0;
    width: 40%;
    height: 100vh;
    padding: 2rem;
    background-color: var(--dark-color);
    font-size: 15px;
    transition: 0.3s;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
}

/* === BUTTONS  === */

.btn {
  display: inline-block;
  background-color: var(--white-color);
  padding: 1.4rem 2rem;
  color: var(--dark-color);
  font-weight: var(--font-medium);
  font-size: var(--font-medium);
  border-radius: 0.5rem;
  transition: 0.3s;
}

.btn:hover {
  transform: scale(1.2);
}

/* === SEARCH === */

.left-navbar {
  display: flex;
  justify-content: flex-end;
}

.search__input {
  display: none;
  height: 2em;
  margin-top: 0.6em;
}

.search__input.active {
  display: inline-block;
}

@media screen and (min-width: 727px) {
}

@media screen and (min-width: 1024px) {
  .nav__toggle {
    display: none;
  }

  .header {
    margin: 0;
    width: 100%;
  }

  .nav {
    margin: 0;
    height: calc(var(--header-height-bigger));
    grid-template-columns: repeat(3, 1fr);
    transition: 0.3s ease-in-out;
  }

  .nav__menu {
    margin-left: auto;
  }

  .nav-list {
    display: flex;
    justify-content: flex-end;
    padding: 0;
    margin: 0;
  }

  .nav-item:hover {
    opacity: 1;
  }

  .nav-list li:hover {
    transform: scale(1.07);
  }

  .nav-item {
    margin-left: var(--mb-6);
    font-size: 1em;
    margin-top: 0.5em;
    padding: 0 0.5em;
  }

  .signup {
    display: block;
    margin-top: 0.5em;
    color: white;
  }
}
</style>