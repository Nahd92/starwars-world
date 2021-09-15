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
.search {
  height: 5em;
  .search-container {
    margin-bottom: -4em;
    .input-icons {
      display: flex;
      justify-content: center;
      position: relative;
      align-items: center;
      .search-input {
        border-bottom: 0.1px solid white;
        border-right: none;
        border-left: none;
        background: transparent;
        width: 100%;
        height: 4em;
        text-align: left;

        &::placeholder {
          font-size: 1em;
          color: #fff;
        }
      }
      input:focus {
        outline: none !important;
        border-color: #719ece;
        box-shadow: 0 0 10px #719ece;
      }
      textarea:focus {
        outline: none !important;
        border-color: #719ece;
        box-shadow: 0 0 10px #719ece;
      }
      input[type="text"] {
        font-size: 1em;
        padding: 0 4em;
        color: #fff;
      }
      .search-icon {
        padding: 0.5em;
        font-size: 1.9em;
        position: absolute;
        top: 0;
        left: 9.5em;
        color: #fff;
      }
      .cross-icon {
        padding: 0.5em;
        font-size: 2em;
        position: absolute;
        right: 9em;
        color: #fff;
        cursor: pointer;
      }
    }
  }
}
</style>