<template>
  <div class="home">
    <HomeIntro text="Cooking Companion" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import HomeIntro from "@/components/HomeIntro.vue"; // @ is an alias to /src

export default Vue.extend({
  name: "HomeView",
  components: {
    HomeIntro,
  },
});
</script>
