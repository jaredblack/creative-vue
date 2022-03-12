<template>
  <div class="content">
    <div class="recipes">
      <div v-for="recipe in recipes" :key="recipe.id">
        <router-link :to="{ path: '/recipe', query: { recipeid: recipe.id } }">
          <div class="recipe-tile">
            <div class="img">
              <img :src="recipe.thumbnail_url" />
            </div>
            <div class="title">{{ recipe.name }}</div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecipeList",
  props: {
    recipes: Array,
  },
};
</script>

<style></style>
