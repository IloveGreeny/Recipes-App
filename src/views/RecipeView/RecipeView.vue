<script setup>

import {onMounted, ref} from "vue";
import axios from "axios";

const recipe = ref([]);




const fetchRecipes = async () => {
  try {
    const recipeId =  this.$route.params.id;
    const response = await axios.get(
        `https://api.spoonacular.com/recipes/${recipeId}/information`,
        {
          params: {
            apiKey: '',//apiKey
          },
        }
    );
    recipe.value = response.data;
  } catch (e) {
    console.log(e);
  }
}


onMounted(() => {
  fetchRecipes();
  console.log(recipe);
});


</script>

<template>

  <div>
    <h2>Recipe Details</h2>
    <div v-if="recipe">
      <img :src="recipe.image" alt="image"/>
      <h3>{{ recipe.title }}</h3>
      <p>{{ recipe.summary }}</p>

    </div>
  </div>
  <h2>{{$route.params.id}}</h2>
</template>



<style scoped>

</style>