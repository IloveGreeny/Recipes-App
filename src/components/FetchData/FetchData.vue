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
});



</script>

<template>

  <div>
    <h1>Recipes</h1>

    <div v-for="recipe in recipes" :key="recipe.id">
      <h1>{{recipe.title}}</h1>
      <img :src="recipe.image" alt="image">
    </div>

  </div>
</template>



<style scoped>

</style>