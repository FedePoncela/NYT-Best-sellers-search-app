<template>
  <section>
    <div class="container">
      <div class="row">
        <div
          class="card col-sm-12 p-2 my-1 wrapper"
          v-for="(book, index) in books"
          :key="index"
        >
          <div id="select" class="d-flex">
            <img
              class="card-img-top shadow-sm bg-white rounded"
              :src="book.book_image"
              alt="Card image cap"
            />
            <div class="card-body d-flex flex-column justify-content-between">
              <h4 class="card-title align-self-center title">
                {{ book.title }}
              </h4>
              <p class="card-text description">{{ book.description }}</p>
              <cite class="font-weight-bold">{{ book.author }}</cite>
              <button v-on:click="redirect(book.title, book.author)">
                More...
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "BookList",
  props: { books: Array },
  methods: {
    redirect: (bookTitle, bookAuthor) => {
      let title = bookTitle.trim().toLowerCase().replaceAll(" ", "+");
      let author = bookAuthor.trim().toLowerCase().replaceAll(" ", "+");

      window.open(
        `https://www.google.com/search?q=${title}+${author}`,
        "_blank"
      );
    },
  },
};
</script>


<style lang="scss" scoped>
$main-black: #464646;
$quickSand-font: "QuickSand", sans-serif;
$poppins-font: "Poppins", sans-serif;

.wrapper {
  border: 1px solid #ffa299;

  #select {
    font-family: $quickSand-font;
    img {
      height: 250px;
      width: 200px;
    }
    img:hover {
      transition: all 0.5s ease;
      transform: scale(1.05);
    }

    .title {
      color: $main-black;
      font-family: $poppins-font;
      font-weight: 600;
    }

    .description {
      color: $main-black;
      font-size: 18px;
    }

    button {
      font-family: $poppins-font;
      font-weight: bold;
      font-size: 16px;
      background: #ff6c5f;
      color: white;
      border-radius: 4px;
      transition: all 0.3s ease-in;
    }
    button:hover {
      background: $main-black;
    }
  }
}

@media screen and (max-width: 620px) {
  img {
    display: none;
  }
}
</style>