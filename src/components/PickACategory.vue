<template>
  <section class="h-100 w-100 d-flex justify-content-center align-items-center">
    <div
      class="w-50 h-50 p-3 d-flex flex-column justify-content-around wrapper"
    >
      <h2 class="text-center title">Choose your favourite</h2>
      <div id="row" class="row h-75 categoryWrapper">
        <div
          v-for="(cat, index) in category"
          :key="index"
          v-on:click="changeBackg"
          class="p-2 col-sm-6 categories"
        >
          {{ cat.list_name }}
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "PickACategory",
  props: {
    category: Array,
  },
  methods: {
    changeBackg: (e) => {
      if (e.target.classList.contains("selectedCategory")) {
        e.target.classList.remove("selectedCategory");
      } else {
        let categories = document.querySelectorAll(".categories");
        for (let i = 0; i < categories.length; i++) {
          categories[i].classList.remove("selectedCategory");
        }
        e.target.classList.add("selectedCategory");
      }
    },
  },
};
</script>


<style scoped lang="scss">

$main-black: #464646;
$quickSand-font: "QuickSand", sans-serif;
$poppins-font: "Poppins", sans-serif;

.wrapper {
  margin-top: 120px;

  .title {
    font-family: $poppins-font;
    font-weight: bold;
    color: $main-black;
    margin-bottom: 20px;
  }

  .categoryWrapper {
    border: 1px solid $main-black;
    border-radius: 4px;

    .categories {
      font-family: $quickSand-font;
      font-weight: 500;
      color: $main-black;
      background: white;
      border: 1px solid $main-black;
    }
    .categories:hover {
      transition: all 0.4s ease;
      cursor: pointer;
      background-color: #ffa299;
      color: white;
      font-weight: bold;
    }
    .selectedCategory {
      background-color: #ffa299;
      color: white;
      font-weight: bold;
    }
  }
}
</style>