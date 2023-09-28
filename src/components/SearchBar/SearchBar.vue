<template>

  <div>
    <input v-model="searchTerm" placeholder="Enter Recipe Title" />
    <button @click="searchRecipes()">Search</button>
    <div v-for="recipe in recipes" v-if="recipes">
      <img :src="`${recipe.image}`" alt="image" width="200"/>
      <h3>{{ recipe.title }}</h3>
      <RouterLink :to="`/recipe/${recipe.id}`">To the Recipe</RouterLink>
    </div>
    <div v-else>
      <h1>Loading</h1>
    </div>
  </div>

</template>


<script setup>


import { ref } from 'vue';
import axios from 'axios';

const searchTerm = ref('');
const recipes = ref([]);

const searchRecipes = async () => {
  try {
    const response = await axios.get('https://api.spoonacular.com/recipes/complexSearch', {
      params: {
        apiKey: '',//apiKey
        query: searchTerm.value,
        number: 5,
      },
    });

    recipes.value = response.data.results;


  } catch (e) {
    console.error(e);
  }

};
</script>




<style scoped>

</style>