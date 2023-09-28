<script setup>

import HomeFetch from "../../components/HomeFetch/HomeFetch.vue";
import SearchBar from "../../components/SearchBar/SearchBar.vue";



</script>

<template>
  <main>
    <RouterLink class="class" to="/">Welcome to Recipes</RouterLink>
    <SearchBar/>
    <HomeFetch/>
  </main>
</template>


<style scoped>
.class {
  text-decoration: none;
  font-size: 24px;
}
</style>