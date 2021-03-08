<template>
  <div
    id="app"
    v-if="!picked"
    class="d-flex flex-column justify-content-center"
  >
    <PickACategory :category="category" />
    <button
      class="w-50 mx-auto cst-btn"
      v-on:click="
        saveCategory();
        picked = true;
      "
    >
      Send
    </button>
  </div>

  <div id="app" class="d-flex flex-column justify-content-center" v-else>
    <SearchBooks :value="value" />
    <button class="w-75 mx-auto cst-btn" v-on:click="picked = false">
      Back
    </button>
  </div>
</template>

<script>
import SearchBooks from "./components/SearchBooks";
import PickACategory from "./components/PickACategory";

import axios from "axios";
import "../node_modules/bootstrap/dist/css/bootstrap.min.css";

export default {
  name: "App",
  components: {
    SearchBooks,
    PickACategory,
  }, //End of components
  data() {
    return {
      category: [],
      picked: false,
      value: "",
    };
  }, //End of data
  mounted() {
    this.getCategory();
  }, //End of mounted
  methods: {
    getCategory() {
      //Geting api info
      axios
        .get(
          "https://api.nytimes.com/svc/books/v3/lists/names.json?api-key=OQSWLHa6QwTxVj0qQJWkLUV7NtKarcfV"
        )
        .then((response) => {
          //Saving first 10 api results into category array to pass as props
          this.category = response.data.results.filter(
            (el, index) => index < 10
          );
        })
        .catch((e) => console.log(e));
    }, //End of getCategory

    saveCategory() {
      //Saving value to pass as props
      this.value = document.querySelector(".selectedCategory").innerHTML;
    }, //End of saveCategory
  }, //End of methods
}; //End of export
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&family=Quicksand:wght@400;500;700&display=swap");

body {
  background: url("../assets/background.jpeg");

  .cst-btn {
    font-family: "Poppins", sans-serif;
    font-weight: bold;
    font-size: 20px;
    background: #ff6c5f;
    color: white;
    border-radius: 4px;
    transition: all 0.3s ease-in;
  }
  .cst-btn:hover {
    background: #464646;
  }
}
</style>
