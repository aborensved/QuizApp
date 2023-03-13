<script setup>
  import { RouterView } from "vue-router";
  import QuizesView from "./views/QuizesView.vue";

  // 6:01:46 - the Ultimate Vue 3 Tutorial (100% composition API)
</script>

<template>
  <div class="container">
    <RouterView />

  </div>
</template>

<style scoped>
    .container {
    max-width: 1000px;
    margin: 0 auto;
  }
</style>