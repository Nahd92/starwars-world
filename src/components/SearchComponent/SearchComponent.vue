<!--PARENT -->

<template>
  <div class="search">
    <div class="search-container">
      <div class="input-icons">
        <input
          type="text"
          v-model="SearchInputField"
          placeholder="Search anything.."
          class="search-input"
          @keyup.enter="submittingInput"
          @keyup.esc="clearSearchField"
        />
        <i class="bx bx-search-alt-2 search-icon"> </i>
        <i
          class="bx bx-x cross-icon"
          v-show="searchValue.length != 0"
          @click="clearSearchField"
        ></i>
      </div>

      <div class="search-text">
        <p v-show="textIsShorterthanThree">
          Atleast 3 characters are required to search, try again!
        </p>
      </div>
    </div>
    <div
      v-show="SearchInputField !== '' && searchValue !== ''"
      class="search-result"
    >
      <SearchResult :searchValue="searchValue" />
    </div>
  </div>
</template>

<script>
import SearchResult from "../SearchComponent/ResultComponent.vue";

export default {
  components: {
    SearchResult,
  },
  name: "SearchComponent",
  data: () => ({
    SearchInputField: "",
    searchValue: "",
    textIsShorterthanThree: false,
  }),
  methods: {
    clearSearchField() {
      this.SearchInputField = "";
      this.searchValue = "";
      this.textIsShorterthanThree = false;
    },
    submittingInput(event) {
      if (event.target.value.length >= 3) {
        this.searchValue = event.target.value;
        this.textIsShorterthanThree = false;
        console.log(this.searchValue);
      } else {
        this.textIsShorterthanThree = true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.search {
  .search-container {
    height: 5em;
    margin-bottom: 5em;
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
        left: 0;
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