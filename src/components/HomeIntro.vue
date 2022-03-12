<template>
  <div>
    <h1
      class="text-8xl py-3 font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-green-500 to-violet-500"
    >
      {{ text }}
    </h1>
    <button
      class="px-4 py-1 text-sm text-purple-600 font-semibold rounded-full border border-purper-200 hover:text-white hover:bg-purple-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-purple-600 focus:ring-offset-2"
    >
      <router-link to="/recipe-book">Get Started</router-link>
    </button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "HomeIntro",
  props: {
    text: String,
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
