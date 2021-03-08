<template>
  <section
    class="h-100 w-100 d-flex justify-content-center align-items-center mt-5"
  >
    <div
      class="w-75 h-50 p-3 d-flex flex-column justify-content-between border border-secondary bg-white wrapper"
    >
      <div class="mb-3">
        <h1 class="h2 title text-center">New York Times Best Sellers</h1>
        <input
          v-on:keyup.enter="categoryPicked"
          class="w-100"
          type="text"
          placeholder="Look for a book title..."
        />
      </div>
      <BookList :books="books" />
    </div>
  </section>
</template>

<script>
import BookList from "./BookList";
import axios from "axios";

export default {
  name: "SearchBooks",
  components: { BookList },
  props: { value: String },

  data() {
    return {
      books: [],
    };
  },
  methods: {
    categoryPicked(e) {
      let apiValue = this.value.trim().replaceAll(" ", "-");
      axios
        .get(
          `https://api.nytimes.com/svc/books/v3/lists/${apiValue}.json?api-key=OQSWLHa6QwTxVj0qQJWkLUV7NtKarcfV`
        )
        .then((response) => {
          this.books = [];
          for (let i = 0; i < response.data.results.books.length; i++) {
            if (
              response.data.results.books[i].title
                .toLowerCase()
                .includes(e.target.value.toLowerCase())
            ) {
              this.books = [...this.books, response.data.results.books[i]];
            }
          }
          e.target.value = "";
          document
            .querySelector(".wrapper")
            .setAttribute("style", "margin-top: 0px");
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>


<style scoped lang="scss">
$main-black: #464646;
$quickSand-font: "QuickSand", sans-serif;
$poppins-font: "Poppins", sans-serif;

.wrapper {
  border-radius: 4px;
  margin-bottom: 16px;
  margin-top: 120px;

  .title {
    font-family: $poppins-font;
    font-weight: bold;
    color: $main-black;
    margin-bottom: 20px;
  }
  input {
    font-family: $quickSand-font;
    border: 1px solid $main-black;
    border-radius: 4px;
  }
}
</style>
