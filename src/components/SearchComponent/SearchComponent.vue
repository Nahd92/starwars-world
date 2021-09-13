<template>
  <div class="search">
    <div class="search-container">
      <div class="input-icons">
        <input
          type="text"
          v-model="search"
          placeholder="Search anything.."
          class="search-input"
        />
        <i class="bx bx-search-alt-2 search-icon"> </i>
        <i
          class="bx bx-x cross-icon"
          v-show="search.length != 0"
          @click="clearSearchField"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchComponent",
  data: () => ({
    search: "",
  }),
  methods: {
    clearSearchField() {
      this.search = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.search-container {
  margin-top: -1.5em;
  .input-icons {
    .search-input {
      background-color: grey;
      width: 100%;
      height: 4em;
      text-align: left;

      &::placeholder {
        font-size: 1.3em;
        color: #fff;
      }
    }
    input[type="text"] {
      font-size: 0.8em;
      padding: 0 4em;
      color: #fff;
    }
    .search-icon {
      padding: 0.5em;
      font-size: 1.7em;
      position: absolute;
      left: 0;
      color: #fff;
    }
    .cross-icon {
      padding: 0.3em;
      font-size: 2em;
      position: absolute;
      right: 0;
      color: #fff;
      cursor: pointer;
    }
  }
}
</style>