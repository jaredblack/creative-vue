<template>
  <div v-if="recipe" class="content">
    <div class="recipe-header">
      <p>{{ recipe.name }}</p>
      <p>{{ recipe.total_time_minutes }}</p>
      <p>{{ recipe.num_servings }}</p>
      <video controls width="50%">
        <source :src="recipe.original_video_url" type="video/mp4" />
      </video>
    </div>
    <div>
      <div v-for="section in recipe.sections" :key="section.position">
        <h1 v-if="section.name === null">Ingredients</h1>
        <h1 v-else>{{ section.name }}</h1>
        <ul>
          <li v-for="ingredient in section.components" :key="ingredient.id">
            {{ ingredient.raw_text }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecipeView",
  data() {
    return {
      recipe: {},
    };
  },
  created() {
    this.recipe = this.getRecipe();
  },
  methods: {
    getRecipe() {
      if (this.$root.$data.recipeList) {
        let recipe = this.$root.$data.recipeList.find(
          (recipe) => recipe.id == this.$route.query.recipeid
        );
        if (recipe) {
          return recipe;
        }
      }
      return this.fetchRecipe();
    },
    fetchRecipe() {
      let apiURL = `https://tasty.p.rapidapi.com/recipes/get-more-info?id=${this.$route.query.recipeid}`;
      console.log(apiURL);
      let recipe = undefined;
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
          recipe = json;
        })
        .catch((err) => {
          console.error(err);
        });
      return recipe;
    },
  },
};
</script>

<style></style>
