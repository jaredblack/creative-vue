<template>
  <div class="about">
    <PicHeader text="Recipe Book" />
    <div id="locator-container">
      <div class="search-form">
        <input
          class="search-bar rounded-md border-2 px-1 py-1 mx-2 my-2 border-gray-400"
          type="text"
        />
        <button type="submit">Search</button>
      </div>
      <div class="locator-buttons">
        <button @click="toggleTags">Search by Tag</button>
        <button @click="getRecipes(null, null, true)">Random Recipes</button>
      </div>
      <TagList v-if="tagsVisible" />
      <RecipeList :recipes="recipes" />
    </div>
  </div>
</template>

<script>
import PicHeader from "@/components/PicHeader.vue";
import TagList from "@/components/TagList.vue";
import RecipeList from "@/components/RecipeList.vue";

export default {
  name: "BookView",
  data() {
    return {
      tagsVisible: false,
      unfilteredRecipes: [],
    };
  },
  components: {
    PicHeader,
    TagList,
    RecipeList,
  },
  computed: {
    recipes() {
      return this.unfilteredRecipes.filter((recipe) =>
        recipe.canonical_id.includes("recipe")
      );
    },
  },
  methods: {
    getRecipes(queryString, tagName, random) {
      let apiURL = "https://tasty.p.rapidapi.com/recipes/list";
      let offset = 0;
      if (random) {
        offset = Math.floor(Math.random() * 8907);
        console.log(offset);
      }
      apiURL += `?from=${offset}&size=30`; // change num recipes?

      if (tagName) {
        apiURL += `&tags=${tagName}`;
      }

      if (queryString) {
        apiURL += `&q=${queryString}`;
      }

      fetch(apiURL, {
        method: "GET",
        headers: {
          "x-rapidapi-host": "tasty.p.rapidapi.com",
          "x-rapidapi-key":
            "0e7f030579msh34a04515a267f43p1cab01jsn0b8b2139c8e7",
        },
      })
        .then((response) => {
          return response.json();
        })
        .then((json) => {
          this.unfilteredRecipes = json.results;
          this.$root.$data.recipeList = json.results.filter((recipe) =>
            recipe.canonical_id.includes("recipe")
          );
        })
        .catch((err) => {
          console.error(err);
        });
    },
    recipeList() {
      return this.$root.$data.recipeList;
    },
    toggleTags() {
      this.tagsVisible = !this.tagsVisible;
    },
  },
};
</script>
