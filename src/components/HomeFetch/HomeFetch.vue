<script setup>

import {ref,onMounted} from "vue";
import axios from "axios";
import {RouterLink} from "vue-router";

const recipes = ref([]);



async function fetchRecipes() {
  try {
    const response = await axios.get('https://api.spoonacular.com/recipes/random', {
      params: {
        apiKey: '',///apikey
        number: 5,
      },
    });

    recipes.value = response.data.recipes;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}


onMounted(() => {
  fetchRecipes();
});




</script>

<template>
  <div>
    <h1>Welcome to Recipes</h1>
    <div  v-for="recipe in recipes" :key="recipe.id">
      <img class="mouse" :src="recipe.image" alt="image" width="200">
      <br>
     <RouterLink :to="`/recipe/${recipe.id}`">To the Recipe</RouterLink>
      <h1>{{recipe.title}}</h1>
      <h2 v-if="recipe.vegan">Vegan </h2>
      <h2 v-else>Not Vegan</h2>
      <p>{{recipe.summary}}</p>
    </div>
  </div>
</template>



<style scoped>



</style>