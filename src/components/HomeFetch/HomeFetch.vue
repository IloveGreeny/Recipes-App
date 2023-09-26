<script setup>

import {ref,onMounted} from "vue";
import axios from "axios";

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
  console.log(recipes);
});



</script>

<template>
  <div>
    <h1>Recipes</h1>
    <div  v-for="recipe in recipes" :key="recipe.id">
      <img :src="recipe.image" alt="image" width="200"/>
      <h1>{{recipe.title}}</h1>
      <h2 v-if="recipe.vegan">Vegan </h2>
      <h2 v-else>Not Vegan</h2>
      <p>{{recipe.summary}}</p>
    </div>
  </div>
</template>



<style scoped>

</style>