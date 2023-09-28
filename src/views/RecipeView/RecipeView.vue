<script setup>

import {useRoute} from "vue-router";
import {onMounted, ref} from "vue";
import axios from "axios";

const recipe = ref(null);

const route = useRoute();


const fetchRecipes = async () => {
  try {
    const recipeId = route.params.id;
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
});


</script>

<template>
  <RouterLink class="class" to="/">Welcome to Recipes</RouterLink>
  <div>
    <h2>Recipe Details</h2>
    <div v-if="recipe">
      <img :src="recipe.image" alt="image"/>
      <h3>{{ recipe.title }}</h3>
      <p>{{ recipe.summary }}</p>
    </div>
    <div v-else-if="!recipe">
      Loading
    </div>
  </div>
</template>



<style scoped>

.class {
  text-decoration: none;
  font-size: 24px;
}

</style>